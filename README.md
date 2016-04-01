# ModalAnimation
一个自定义的Modal转场，Object-C实现

####目前主流的自定义转场
>1. 在` UINavigationController `中  ` Push 和 Pop`
2. 在 `UITabBarController `中切换 `TabBar`
3. 模态(Modal) 转场：`Present 和 Dismiss`，仅限于`modalPresentationStyle`属性为 `UIModalPresentationFullScreen `或` UIModalPresentationCustom `这两种模式
4. `UICollectionViewController` 布局转场(与 `UINavigationController `结合的转场方式)

####转场动画的实现
转场协议由5种协议组成，在实际开发中只需我们提供其中的两个或三个便能实现绝大部分的转场动画。
- 1.转场代理(Transition Delegate) - 必须使用：
自定义转场的第一步便是提供转场代理，告诉系统使用我们提供的代理而不是系统的默认代理来执行转场，不同类型的控制器遵守的协议不同，如下：

```
/**
 *  除了<UIViewControllerTransitioningDelegate>是 iOS7 新增的协议，其他两种在 iOS2 里就存在了
 */
<UINavigationControllerDelegate> //UINavigationController 的 delegate 属性遵守该协议
<UITabBarControllerDelegate> //UITabBarController 的 delegate 属性遵守该协议
<UIViewControllerTransitioningDelegate> //UIViewController 的 transitioningDelegate 属性遵守该协议
```

- 2.动画控制器(Animation Controller)  - 必须使用：
最重要的部分，遵守`<UIViewControllerAnimatedTransitioning>`协议，负责添加视图以及执行动画，由我们实现
- 3.交互控制器(Interaction Controller) - 可选使用：
通过交互手段，通常是手势来驱动动画控制器实现的动画，使得用户能够控制整个过程；遵守`<UIViewControllerInteractiveTransitioning>`协议
- 4.转场环境(Transition Context) - 必须使用:
提供转场中需要的数据；遵守`<UIViewControllerContextTransitioning>`协议；由` UIKit `在`转场开始前生成`并提供给我们提交的动画控制器和交互控制器使用
- 5.转场协调器(Transition Coordinator) - 可选使用：
可在转场动画发生的同时并行执行其他的动画，主要在 Modal 转场和交互转场取消时使用，其他时候很少用到,由 UIKit 在转场时生成，遵守`<UIViewControllerTransitionCoordinator>`协议；UIViewController 在 iOS 7 中新增了方法`transitionCoordinator()`返回一个遵守该协议的对象，且`该方法只在该控制器处于转场过程中才返回一个此类对象，不参与转场时返回 nil`

详情见我的简书[iOS之实现自定义转场动画](http://www.jianshu.com/p/cc548a5fe42f)
