# Parcelable 重复读取字段导致后续序列化数据读取失败 (java.lang.RuntimeException: Parcel android.os.Parcel@xxx: Unmarshalling unknown type code xxx at offset xxx)

在做项目过程中遇到了一个奇葩的问题。
1. 开发者模式打开不保留后台活动
2. 打开 Activity 再打开 Fragment
3. 