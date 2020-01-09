# **Variant使用**

适用于苏标中表格变量的存储与序列化

- 初始化

  ```
  std::string types[11]={"DWORD", "DWORD",  "DWORD", "DWORD", "WORD",    	  						"WORD","WORD",  "BCD[6]", "BYTE",  "STRING", "BYTE[6]"};
  Variant pos_variant(types, 11);
  ```

  构造函数`Variant(string [], int param_num)`

  参数1：string [] ,表格中各个数据的数据类型，按顺序

  参数2：param_num, 数据个数

  

-  设置变量

  ```
  fab_uint32 warning = 23;
  pos_variant.SetValue(0, warning)
  ```

  `fab_bool SetValue(fab_int32 i, T value)`

  i : 数据在表格中的索引（0开始）

  value: 设置的值

  返回值：成功 true ；失败 false

  注：值的类型与表格的类型要相对应，表中数据类型与C++ 数据类型的对应关系如下

| 表 type    | aibox type     |
| ---------- | -------------- |
| DWORD      | fab_uint32     |
| WORD       | fab_uint16     |
| BYTE       | fab_uint8      |
| BYTE[n]    | fab_uchar a[n] |
| BCD[n]     | fab_uchar a[n] |
| STRING     | std::string    |
| STRING(id) | std::string    |

注：STRING(id)为自己定义表格格式，表示变长STRING，其中id标识协议表格中第id字段为此STRING长度

- 获取变量

  ```
  fab_uint32 get_varning;
  pos_variant2.GetValue(0, get_varning);
  ```

  

- 序列化

  ```
  //初始化以及设置好变量后
  pos_variant.SerializeVariant();
  ```



- 获取序列化值

  ```
  std::vector<fab_uchar> seriral_v;
  pos_variant.GetSerializeVariant(seriral_v)
  ```



- 反序列化

  ```
   Variant pos_variant2(types, 11);
   pos_variant2.DeserializeVariant(seriral_v); 	// serial_v 是序列化后的vector
   
   // fab_uint32 get_varning;
   // pos_variant2.GetValue(0, get_varning);
  ```

  

