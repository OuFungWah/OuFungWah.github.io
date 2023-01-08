# 一些 Fragment 的源码级别 Crash 收集
## Q: 在 `Fragment` attach 之前或已经 detach 的时候尝试获取 `childFragmentManager`
A: 在尝试获取 `ChildFragmentManager` 时会判断当前 `Fragment` 是否已经 attached. **是个坑点**. 例如说: 尝试在 `onDestroy` 上获取 `childFragmentManager` 去操作子 `Fragment`
> 源码位置: androidx.fragment.app.Fragment#getChildFragmentManager