# Fragment
## 介绍
## 踩过的坑
  1. 1）Fragment getParentFragmentManager 在 Fragment 已经 detach 后调用会 crash。常见于 dialog dismiss 后去拿 Fragment Manager 做点什么。留意 Fragment 中的各种回调，是否在 Fragment 生命周期结束时已经取消监听了，或者是否在回调中添加了 Fragment 状态判断，谨慎处理。
  2. 2）Fragment 重复添加，同一个 TAG 或者同一个 Fragment 对象已经在 Manager 中了，再次调用 addFragment，会 crash。常见于应用后台被杀了以后，重新回到前台时，系统自动回复的 Fragment 和代码中的 add 动作重复了。需要加 isAdded 保护，或者在 add 之前先把重复的 tag 移除掉