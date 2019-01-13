# Curl命令使用

curl全称"CommandLine Uniform Resource Loactor", curl是命令方式下工作，利用url的愈发进行数据的传输或文件传输。


## 常用参数说明

| 参数　　　     | 含义　　　                                                                      | notes                                         |
|----------------|---------------------------------------------------------------------------------|----------------------------------------------|
| `-v --verbose` | 指定该选项后，可以跟踪URL的连接信息。我们可以根据这个选项看看curl是怎么工作的。 |  常用于观察交互过程                                            |
| -X HTTP方法    | 指定请求方法                                                                    |                                              |
| -i             | 显示response header                                                             |                                              |
| `-I`           | 只显示响应头部                                                                  |                                              |
| -d /--data     | 设定数据                                                                        |                                              |
| `-C`           | 断点续传                                                                        | `curl -C -o testxxx url`                     |
| `-O`           | 使用原名称                                                                      | `curl -O http://test.com/1.jpg`              |
| `-o`           | 自定义文件名                                                                    | `curl -o hello.jpg http://test.com/1.jpg`    |
| `-x`           | 设置代理                                                                        | `curl -x -o hello.jpg http://test.com/1.jpg` |
| `-e`           | 设置refer字段                                                                   |                                              |
| `-H`           | 设置请求头参数                                                                  |                                              |
| `-F`           | 模拟表单登录                                                                    |                                              |
| `-r`           | 可以进行分段下载                                                                |                                              |
| `-c`           | 保存cookie信息                                                                  |                                              |


## 例子


**使用不同方法访问url**

```
curl -X GET "http://www.baidu.com"
curl -X POST "http://www.baidu.com"
curl -X PUT "http://www.baidu.com"
curl -X DELETE "http://www.baidu.com"
```

**Post数据到REST资源**


```
curl -i -H "Accept: application/json" -X POST -d "name=yhh&age=18" http://xxxx/persons/person
```

**Put资源**

```
cuil -i -H "Accept: application/json" -X PUT -d "name=yxx" http://xxx/persons/person
```


**处理json格式**

```
curl url | python -m json.tool
```

**批量模式**

```
$curl -O "http://www.text.com/curl/[1-100].jpg"
$curl -O "http://www.test.com/curl/[1-100:10].jpg"
```


**分割下载**

```
$curl -r 0-40960 -o "rose.part1" "http://blueapple.infor.org/rose.jpg" 
curl -r 40961-81920 -o "rose.part2" "http://blueapple.infor.org/rose.jpg" 
curl -r 81921-125068 -o "rose.part3" "http://blueapple.infor.org/rose.jpg"
```
