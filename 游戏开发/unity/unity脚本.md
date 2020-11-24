# 基础

## 基本结构

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class NewBehaviourScript : MonoBehaviour
{
  void Start()
  {

  }

  void Update()
  {

  }
}
```

## unity脚本运行的基本原理

unity脚本是创建一个类，但是并没有实例化，要想运行就必须实例化一个对象，这个对象的创建就是靠挂载到游戏对象完成的。把脚本拖到对象上时，系统自动创建一个对象，然后把引用返回给游戏对象，这时在inspector中就有了这个脚本。其实inspector中的那些组件和脚本都是对象的引用，Transform其实就是Transform类的对象，而挂载这些组件的游戏对象其实就是一个特殊的数组，里面存放着很多对象的引用，需要时会自动访问这些对象。

# unity脚本的生命周期

unity脚本是挂在在游戏物体上的，物体有生命周期，脚本当然也有了。

unity脚本的生命周期是unity开发中必须掌握的重要内容。

## 初始化

- Awake：

  当游戏对象创建时，立刻执行，可以判断是否可以启用脚本。

- OnEnable:

  每当启用脚本时调用，注意启用表示可以调用，并不是调用。

- Start： 

  游戏对象调用脚本时执行

## 物理处理

- FixedUpdate：

    它是物理循环中最先执行的函数，它每隔固定时间执行一次。我们通常与把物理模拟有关的代码，写在 FixedUpdate 函数中，比如给游戏对象添加力。默认0.02s执行一次。

- OnTrigger：

-  OnCollision：

## 接收鼠标事件

- OnMouseXXX：

  有关鼠标的函数就在此刻执行。

## 游戏逻辑处理

- Update：

  它在每帧执行一次，该函数主要处理游戏对象在游戏世界的行为逻辑，例如游戏角色的控制和游戏状态的控制.

- LateUpdate： 

  它也是每帧执行一次，在 Update 函数后执行。 在实际开发过程中 Update 函数与 LateUpdate 函数通常共同使用。一般我们在 Update 函数中处理玩家角色的移动，在 LateUpdate 函数中处理摄像机跟随玩家，这样能防止摄像机出现抖动现象。因为，如果我们把这两个都写在Update中，有可能造成摄像机先跟随，玩家后移动的逻辑bug。 

## 场景渲染

- OnBecameVisible/OnBecameInvisible：

  当物体在任何相机中可见/不可见时调用。注意：Scene视图的相机也需要考虑进去。

## GUI渲染

- OnGUI：

  一帧会调用多次来响应GUI事件。

## 停用脚本

## 析构

- OnApplicationQuit：

  应用退出时所有的游戏物体将会调用此函数

- OnDestroy：

  脚本或者脚本挂载的游戏对象销毁时，在对象存在的最后一帧调用。