# Parcelable 重复读取字段导致后续序列化数据读取失败 (java.lang.RuntimeException: Parcel android.os.Parcel@xxx: Unmarshalling unknown type code xxx at offset xxx)

在做项目过程中遇到了一个奇葩的问题。

1. 开发者模式打开不保留后台活动
2. 打开 Activity 再打开 Fragment
3. 系统恢复 Fragment 时，在尝试从 arguments 中读取某个参数时崩溃了。

具体报错信息：

```

```

> 排查过程：
> 1，优先判断是否为线上问题（使用线上包复现路径）
> 2，其次判断什么时候引入的（对比 release 包、对比 dev 包、对比上版本包）
> 3，查看无问题到有问题之间版本的可疑提交


