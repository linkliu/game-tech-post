---
title: "Unity的Addressables学习日志"
date: 2023-08-29T15:45:15+08:00
categories: ["Unity"]
tags: ["U3D", "Unity", "Addressables "]
author: "LINK"
---

- **1.构建Player的时候，项目的资产数据是如何放进Player中的**   
  由下图可以看出来Unity中的资产分成了4个主要类别：   
  - 1.被场景引用的资源
  - 2.放在Resources文件夹中的资源
  - 3.标记为了Addressables Group的资源
  - 4.放在了StreamingAssets文件夹中的资源
  ![diagram](/game-tech-post/img/unity3d/addr_interact_baloons.png) 

- **2.如果同一个资产被划分到了不止一个类别上，那么该资产在构建的时候就会产生重复，划分了多少个就会复制多少个**
- **3.Addressables Groups中的共享资产**   
  对于一个标记为非Adressables的资产，如果有不止一个Adressablees的资产引用了它，那么它会在每个引用了它的Addressables的bundle中都复制一份。如下图所示：   
  ![diagram](/game-tech-post/img/unity3d/addr_interact_shared.png)    
  为了消除这种复制，那么可以将这个共有的资产也标记为Addressables。然后把它引入到一个已存在的bundle中就可以了。如果此时一个bundle要引用它，那么必须在该bundle实例化前，将引入了共有资产的bundle先加载才可以。   
- **4.Sprite的依赖**   
  图集的引用跟其他资产不一样。
  - 情形一   
  三张纹理，分别在三个不同的group中，它们会分别进入三个不同的ab包，彼此之间没有依赖，每个ab中图片的大小是500KB
  ![diagram](/game-tech-post/img/unity3d/addr_share_exa1.png)    
  - 情形二   
  还是这三张图片，它们被放进了一个图集，这个图集没有被标记为Addressables。那么包含这个图集的ab包将有图集的1500KB的大小。而另外两个ab包则只包含Sprite的元数据（只有很小的几KB），并且将包含图集的ab包列为自己的依赖。无论是哪个ab包包含这个图集，在重新构建之后都是跟前面一样的结果，这个过程由Unity控制，用户决定不了。这是跟标准的处理依赖重复资源过程的最大不同。Sprites的加载依赖它的图集，而图集的加载只依赖包含它的ab包的加载。   
  ![diagram](/game-tech-post/img/unity3d/addr_share_exa2.png)    
  - 情形三   
  在上面的情形二的基础上，图集被标记成了Addressables并且单独放在它自己的图集中。这时候就会创建4个ab包。如果使用的是Unity2020.x或者更新的版本，那么在构建之后，4个ab包之间的依赖关系会和期待的一样，即图集资源在图集的这个ab包，有1500KB。另外三个ab包把图集的ab包作为依赖，只有几KB的引用数据而已。如果使用的是Unity2019.x或者更旧的版本，那么纹理资源就可能存在于这4个ab包中的某一个。另外三个ab包依然把图集所在的ab包作为依赖。然而此时图集所在的ab包可能仅仅只包含了图集的一些元数据，而真正的纹理资源可能在其他的另外3个ab包中。

- **5.Addressable预制体跟Sprite的依赖**   
  - 情形一   
  跟三个标记为Addressables的纹理不同的是，这里是三个标记为Addressables的Sprite的预制体。每个预制体包含它独自的Sprite。在构建之后，三个ab包的大小如期望的那样，都是500KB。
  - 情形二   
  跟情形一类似，3个预制体分别引用不同的Sprite，只不过所有的3个Sprite添加到一个图集中，但是这个图集没有标记为Addressables。在这种情形下，图集的纹理机会产生重复。在构建之后，三个ab包都大概有1500KB。这个重复资源的规则类似于一般的Addressables重复资源规则，但是跟前面介绍的 **Sprite的依赖** 中的情形二又不一样。
  - 情形三   
  基于上面的情形二的预制体，纹理和图集，不过这里把图集标记为Addressables。此时图集纹理就仅仅只存在在包含图集的ab包中。另外的三个预制体的ab包就把这个图集的ab包作为依赖。

- **6.ab包的分包规则**   
  - 1.可以将一个group中所有Addressables的资源都打进一个ab包中
  - 2.可以将一个group中的每个Addressables资源分别打进它独自的ab包中
  - 3.可以将使用同一个label的所有的Addressables资源打包进一个ab包中

- **7.同一个group中的场景资源会跟其他的Addressables资源分开打包**   
  也就是说一个group中如果含有场景资源和其他非场景资源，那么构建之后，至少会得到两个bundle，一个包含场景资源，一个是除了场景外的其他资源。