# Lua ip2region binding

### 一，如何测试
* 1, cd到ip2region/binding/lua/根目录
* 2, 运行testSearcher测试程序
```shell
lua testSearcher.lua ../../data/ip2region.db
```
* 3, 输入ip地址开始测试即可
```shell
initializing btree
+----------------------------------+
| ip2region test script            |
| Author: chenxin619315@gmail.com  |
| Type 'quit' to exit program      |
+----------------------------------+
ip2region>> 1.2.3.4
0|美国|0|华盛顿|0|0 in 8.001000 millseconds
ip2region>> 101.233.153.103
2163|中国|0|广东省|深圳市|鹏博士 in 0.176000 millseconds
ip2region>>
```


### 二，如何使用
* 1, 将Ip2region.lua拷贝到你的package.path下
* 2, 通过如下流程在你的lua程序中使用
```lua
-- 包含模块
require "Ip2region";

-- 创建查询对象
-- dbFile表示ip2region.db数据库文件的地址
local searcher = Ip2region:new({dbFile: "ip2region.db file path"});
local data;

-- 查询，备注请使用“:”调用方法，不要使用“.”
-- 1，binary查询
data = searcher:binarySearch("101.233.153.103");

-- 2，btree查询
data = searcher:btreeSearch("101.233.153.103");

-- 3，memory查询
data = searcher:memorySearch("101.233.153.103");

-- 返回结果如下
print("city_id=", data.city_id, "region=", data.region);
```

### 三，备注
* 1，Ip2region模块的位运算依赖了bit32模块，这个是lua 5.2才开始支持的。
