## 一、使用步骤总结：

1. 注册驱动 依赖的jar包，进行安装
2. 建立连接 connection
3. 创建发送SQL语句的对象statement
4. statement对象，发送SQL语句到数据库，并且获取返回结果
   结果对象 resultset
5. 解析结果集
6. 销毁资源 释放connection 释放statement 释放resultset