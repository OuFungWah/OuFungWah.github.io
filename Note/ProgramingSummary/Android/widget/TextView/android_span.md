# Span --- 文本的修饰片段
* 是什么
    * 官方解释
    * 说人话
* 为什么
    * 用处
        * 文案中的链接
        * 表情包
    * 必要性
* 怎样用
    * 常见用例
        * Span
        * Spannable
        * Spanned
        * SpannableStringBuilder
    * 原理
        * Span 的绘制原理
## Span 是什么

Span，译作「跨距」，「常用内联容器」，「量程」，在 Html 中，它叫**行内元素**（个人感觉更贴切）。可用作 TextView 中指定文案的修饰，例如将部分文字转换为图片；将部分文字高亮或者加下划线；为部分位置添加特定点击事件...等等。

Android 原生提供了数种强大的 Span 供我们使用，ClickableSpan, ImageSpan, ForegroundColorSpan...。当原生的 Span 无法满足我们的需求时还可以通过继承的方式去实现我们想要的效果。

> Spans are powerful markup objects that you can use to style text at a character or paragraph level. By attaching spans to text objects, you can change text in a variety of ways, including adding color, making the text clickable, scaling the text size, and drawing text in a customized way. Spans can also change TextPaint properties, draw on a Canvas, and even change text layout.
> Android provides several types of spans that cover a variety of common text styling patterns. You can also create your own spans to apply custom styling.