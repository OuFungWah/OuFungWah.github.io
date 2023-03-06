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
## Android Span 的架构


* CharacterStyle，所有 Span 的父类
    * android.text.style.CharacterStyle#wrap，一个 Span 对象只可以依附在单一区域中，如果需要再多段区域使用同一个 Span，可以通过 wrap 方法给 Span 对象包裹一层，从而解决冲突问题。
* CharacterStyle
    * 支持的 View：EditText、TextView
    * 外观类型子类：
        * ForegroundColorSpan：前景色（字体颜色）
        * BackgroundColorSpan：背景颜色（文字背景色）
        * MaskFilterSpan：滤镜（设置 filter 可实现高斯模糊效果 BlurMaskFilter、浮雕效果 EmbossMaskFilter、阴影效果）、
        * MetricAffectingSpan：抽象的，可改变文字大小的 Span 的父类，例如：ImageSpan, AbsoluteSizeSpan。
        * StrikethroughSpan：删除线
        * SuggestionRangeSpan：Unknown（待实验）
        * SuggestionSpan：Unknown（待实验）
        * UnderlineSpan：下划线
    * 行为类型子类
        * ClickableSpan：可点击 Span
    * Unknown：Cea708CaptionRenderer
* 冷知识：Html 使用的也是 Spanned


## Span 是什么

Span，译作「跨距」，「常用内联容器」，「量程」，在 Html 中，它叫**行内元素**（个人感觉更贴切）。可用作 TextView 中指定文案的修饰，例如将部分文字转换为图片；将部分文字高亮或者加下划线；为部分位置添加特定点击事件...等等。

Android 原生提供了数种强大的 Span 供我们使用，ClickableSpan, ImageSpan, ForegroundColorSpan...。当原生的 Span 无法满足我们的需求时还可以通过继承的方式去实现我们想要的效果。

> Spans are powerful markup objects that you can use to style text at a character or paragraph level. By attaching spans to text objects, you can change text in a variety of ways, including adding color, making the text clickable, scaling the text size, and drawing text in a customized way. Spans can also change TextPaint properties, draw on a Canvas, and even change text layout.
> Android provides several types of spans that cover a variety of common text styling patterns. You can also create your own spans to apply custom styling.

## 