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
* DialogFragment show 方法
    * `dialog.show(supportFragmentManager, "dialog")`
        * 猜测：该 Fragment 只做生命周期管理，并不实际渲染。
    * 将 Fragment 对象提交到了对应的 FragmentManager
    * 提交后走 Fragment 生命周期
        * onCreate 尝试恢复 bundle 中的数据
        * onGetLayoutInflater，创建 LayoutInflater 的方法。在 DialogFragment 中就顺带创建了 Dialog
        * onCreateDialog，创建 Dialog，重写该方法生成想要的 Dialog。
        * onCreateView，在不重写 onCreateDialog 时，该方法用于指定 Dialog 的 contentView
        * onStart, 常规的 Fragment 回调，在此处做了 Dialog show 的方法
            * `mDialog.show();`
        * onResume 无特殊处理

* 

* DialogFragment 生命周期

``` kotlin
// show dialog
onCreate
onGetLayoutInflater
onCreateDialog
onCreateView
onStart
onResume

// dismiss dialog
pnPause
onStop
onDestroyView
onDestroy
```