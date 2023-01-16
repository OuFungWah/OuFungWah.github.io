# Asset 资源

Asset 译作资产， 放到 Android 的上下文中他指的是 Android App 中自己携带的一些资源文件。

有别于 Drawable，Asset 对存放在内部的文件更加的宽容，且 Asset 仅仅是被打包到 apk 中，但并不会被编译成资源文件并生成 ID， 如果某些内容希望在运行时获取到源文件，那么放在 Asset 中是比较理想的（例如一些静态网页 html 文件， 又或者 Lottie 动画的 json 文件等等）。

Asset 与 Drawable 的区别:

|区别|Drawable|Asset|
|:-:|:-:|:-:|
|文件类型|xml/png/jpg/webp/.9|支持所有文件|
|编译|编译成 resource.arsc 文件以及索引 R.java|直接带入 apk|

## 使用例子 Some Example

### 0，assets 目录结构
* assets 是一个与 main 平级的文件夹，里面可以有更多的文件目录层级，取决于是否有对应的文件归类管理需求（一般都会有）。文件夹一般需要自己新建。

```kotlin
xxx_module
    main
        assets
            lottie
                bell_anim.json
                click_anim.json
            test1.png
            test2.png
        java
        res
```

### 1，通过 AssetsManager 打开对应的 Asset 文件

* 从 Context 中获取 assetManager 用以打开 InputSteam。有 InputSteam 你就可以做你想做的事情了，用对应的解析器来讲输入流转为你想要的数据对象。例如例子中的 Bitmap。

```kotlin
try {
    val assetsManager = context.assets
    val inputSteam = assetsManager.open(fileName)
    val bitmap = BitmapFactory.decodeStream(inputSteam)
    inputSteam.close()
} catch (t: Throwable) {
    // do something while failed.
}
```

### 2，通过 Uri 的方式找到 Asset 文件

* 某些场景下我们需要用到文件的 Uri，此时我们需要自己拼接对应的协议，`asset://[$path/][$file_full_name]`。例如：我们希望用 WebView 加载一个位于 Asset 的 html 静态网页，又或者说用 Fresco 加载一个 asset 的图片资源。

```kotlin
// 如果是放在了根目录，则不需要 path，但是 path 对应的 '/' 需要加上
val webUri = Uri.parse("asset:///index.html")
webview.loadUrl(webUri)

// 如果是放在了深层级的目录，则把完整的目录路径加上
val iamgeUri = Uri.parse("asset://emoji/laugh.png")
simpleDraweeView.loadUrl(imageUri)

```