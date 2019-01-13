# 1.选项

## 1.1 基础选项

+ -b / --background 
+ -n
+ -o logfile  Log all messages to logfiles
+ -q / --quiet  Turn off wget's output
+ -i file   Reads urls from a local or external file

## 1.2 下载选项

+ -t number Set number of retries to number
+ -c Continue
+ -T seconds / --timeout=seconds Set timeout 
+ --user=user
+ --password=password

## 1.3 目录选项 

+ -nd 
+ --no-directories    Do not create a hierarchy of directories when retrieving recursively.
+ -np not recurise parent directories

## 1.4递归选项

+ -r
+ --recursive		Turn on recursive retrieving. The default maximum depth is 5.
+ -l depth
+ --level=depth

# 2. 常用命令

```
	wget -r -nd -np url
	wget -r -nd -np --accept=iso url
	wget -c url
```
