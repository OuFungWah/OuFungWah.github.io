# Module using application's plugin
在开发过程当中, 普通的 Module 应该使用 ```com.android.library``` 的 Plugin, 但是错误地将 Module 的 plugin 写成 `com.android.application` 系统将会按照 App 的方式去编译当前 Module (Module 肯定缺少了一些 App 独有的信息) 会报资源找不到的 AAPT 资源链接错误.

# Reference
* [StackOverFlow: A dependent feature was defined but no package ID was set. You are probably missing a feature dependency in the base feature](https://stackoverflow.com/questions/45891659/a-dependent-feature-was-defined-but-no-package-id-was-set-you-are-probably-miss)