---
title: "Unity的Addressables使用体验"
date: 2024-11-07T10:08:24+08:00
categories: ["Unity"]
tags: ["U3D", "Unity", "Addressables "]
author: "LINK"
---

之前大致的了解了Addressalbe这个插件的大致功能和原理，并没有深入的使用。刚好这段时间有时间，就按照具体的项目场景搭建了一个简单的框架来体验。我是用它跟XLua来搭建整个游戏的框架的。Addressables的版本是1.22.3。我的体验也是围绕这个版本来讲的。使用的过程中发现它的下面几个问题，让我觉得目前还是不要在项目中使用它。   

- **1.性能问题**   
  **通过标签一次性加载大量粒度很细的文件，会非常的慢。**
  Adressables可以通过lable标签来加载同一类型的资源。比如在项目中，把所有类型的lua文件都打上 `<Lua>` 标签。你可以选择 `Addressables.LoadResourceLocationsAsync` 先获取所有打了该标签的文件地址，然后再用一个循环去加载每一个地址的lua文件，然后把文件按照Key-Value的方式存在一个字典中。也可使用 `Addressables.LoadAssetsAsync<Type>("key"), (asset)=>{}` 方式按照标签加载所有的资源，然后在它里面的回调中去处理每一个lua文件，并保存到字典。这个回调每加载一个该标签下的文件，都会回调一次。   
  很显然，这个加载循环无法避免。由于lua文件的数量巨大，导致这个循环完成非常的耗时，比如在这次测试的项目中，总共有接近**400**个lua文件，总耗时在**webgl**平台达到惊人的 **5.89** 秒，并且随着功能的增多，这个数量只会往上加。这是很难接受的。android和IOS我没有测试，不过由于多线程的加持，估计是很快的。我们的主要平台是webgl.
- **2.工具黑盒**   
  这个插件并不是开源的，对于用户来说，**资源的下载，打包过程都是不受用户控制的。也就是说，它对用户来说是一个黑盒**。他在官网有用户手册和API说明，但也就仅仅是那些而已。我甚至觉得这个东西不是为游戏开发者准备的，更像是一个功能说明。它的加载API少的非常的可怜，估计也就3个左右吧，不知道是不是我看的不够仔细，我真的没有再发现别的加载API了。而且API设计的很模糊，太多的功能细节集中到一个API上了，然后例子又少。虽然GitHub上有官方的示例，但我真的还是第一次见到如此模糊的API设计，我真的无法通过参数去了解该API到底能做什么事情。   
  用户没有办法了解其中具体的细节，也没有办法去定制项目需要的功能，万一有一些东西满足不了项目的需求需要修改，就只能干着急，你做不了任何事情。它的封装级别很高，但是对于游戏开发者来说，这过头了。这个插件更像是面向产品用来设计快速原型的产物。就拿上面的第一个问题来说，所有的lua其实已经打在一个AB包里面了，那么AB包下载之后，再从AB包中去加载lua文件，应该是非常的快的（毫秒级别），但不知道为什么，400多个文件加载居然要5.89秒，它里面是不是每一个文件加载都去走了什么特殊流程导致非常的慢。然后勾选了缓存，第二次，第三次，第四次的时间也是一样的，居然没有任何的时间减少。用户知道的太少了。
- **3.各种的小问题**   
  我这里例举一个下载进度的问题。
  ```c#
    public IEnumerator LoadAssetAsyn(string key, Action<Object> completeCB, Action<float> pgrFunc = null)
    {
        AsyncOperationHandle<Object> opHandle;
        opHandle = Addressables.LoadAssetAsync<Object>(key);
        while (opHandle.Status == AsyncOperationStatus.None)
        {
            Log.Error("Percent=" + opHandle.GetDownloadStatus().Percent + " pp=" + opHandle.PercentComplete);
            if (pgrFunc != null)
            {
                pgrFunc(opHandle.GetDownloadStatus().Percent);
            }
            yield return null;
        }
        yield return opHandle;
        if (opHandle.Status == AsyncOperationStatus.Succeeded)
        {
            Object instObj = Object.Instantiate(opHandle.Result);
            completeCB(instObj);
            if (pgrFunc != null)
            {
                pgrFunc(1);
            }
        }
        yield return null;
    }
  ```   
  上面的这个方法去加载一个资源，然后通过回调告诉目前的下载进度。`opHandle.GetDownloadStatus().Percent` 和 `opHandle.GetDownloadStatus().Percent` 都不准确。前者是通过大小计算百分比，后者是通过数量计算百分比。   
  
  ***
  下面是文档的原话：   
  **AsyncOperationHandle.PercentComplete:** Reports the percentage of sub-operations that have finished. For example, if an operation uses six sub-operations to perform its task, the PercentComplete indicates the entire operation is 50% complete when three of those operations have finished (it doesn't matter how much data each operation loads).   
  **AsyncOperationHandle.GetDownloadStatus:** Returns a DownloadStatus struct that reports the percentage in terms of total download size. For example, if an operation has six sub-operations, but the first operation represented 50% of the total download size, then GetDownloadStatus indicates the operation is 50% complete when the first operation finishes.   
  


  我们在编辑器内运行模式选择从AB包运行：   
  <div align="center"><img src="https://linkliu.github.io/game-tech-post/assets/img/unity3d/addressables_1.png"/></div> 




  我们看日志输出:
  <div align="center"><img src="https://linkliu.github.io/game-tech-post/assets/img/unity3d/addressables_2.png"/></div> 

  `Percent` 表示加载的大小百分比，`pp` 表示文件数量的百分比。很显然是不对的，前者一直是0，然后加载完之后就立马变成了1，后者是数量百分比，反而是从0开始一直一点一点的增加，最后变成1。感觉像是这两个数字恰好反过来了一样。不知道是不是真的反过来了还是计算本身就是错的，没有源码也根本就不知道。不能让开发者去猜测的。这个问题，我也在网上查阅了很久，遇到这个问题的开发者有很多，而且在不同的release版本都有。这种问题应该是比较低级的，不应该出现在release版本中。


***

也不知道还有没有其他未发现的问题，但是在项目中使用不成熟和不稳定的东西是非常的危险的，所以就目前的体验来开，Addressables不适合用在项目中，自己拿来玩一玩是可以的。
