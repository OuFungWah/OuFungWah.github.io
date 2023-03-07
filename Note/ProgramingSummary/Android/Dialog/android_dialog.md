# Dialog

## Dialog 和 DialogFragment 区别

想要了解 Dialog 和 DialogFragment 之间的区别，我们需要先了解两者本身是什么

### Dialog 是什么？

Dialog 是由 Activity 管理的，悬浮于管理者 Activity 之上的一个组件。它有自己单独的 Window，该 Window 的层级比其拥有者 Activity 要高

* 创建 Dialog：配置 theme、新建 Window 对象、新建 ListenersHandler
    * ListenersHandler 通过接受来自主线程的 show、dismiss、cancel 等动作向对应的业务配置的 listener 发送事件，从而做出回调的效果（主线程回调）
* 调用 Show 方法
    * 检测是否已 show
    * 是否已创建：
        * no：onCreate()。首次创建需要手动调用 setContentView，为 window 提供内容渲染
    * onStart：每次 show 都会调用
* 调用 dismiss 方法
    * 检测是否已 dismiss
    * 使用 windowsManager 立刻移除 DecorView
    * mDecor 置空
    * onStop()

### DialogFragment 是什么

DialogFragment 本质上就是 Fragment，使用 Fragment 的各种生命周期管理一个 Dialog

* 创建：
    * 就是一个普普通通的 Fragment 创建