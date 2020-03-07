Given a text file `file.txt` that contains list of phone numbers (one per line), write a one liner **bash** script to print all valid phone numbers.

You may assume that a valid phone number must appear in one of the following two formats: (xxx) xxx-xxxx or xxx-xxx-xxxx. (x means a digit)

You may also assume each line in the text file must not contain leading or trailing white spaces.

Example:

Assume that `file.txt` has the following content:
```
987-123-4567
123 456 7890
(123) 456-7890
```
Your script should output the following valid phone numbers:
```
987-123-4567
(123) 456-7890
```

---
### Solution
**正则表达式** Regular Expression
#### Approach 1: using _grep_
- grep 命令被用来**检索一台服务器或工作站上任何位置的文本信息**
- -P：表示打印操作（？存疑）
- ^：开始标记
- $：结束标记
- \d：表示数字
- {N}：匹配前一个字符N次
```Bash
grep -P '^(\d{3}-|\(\d{3}\) )\d{3}-\d{4}$' file.txt
```
8 ms, faster than 25.20% ; 3.1 MB, less than 96.43% 

#### Approach 2: using _awk_
- awk：一个强大的文本分析工具，在对文本文件的处理以及生成报表，awk是无可替代的。awk认为文本文件都是结构化的，它将每一个输入行定义为一个记录，行中的每个字符串定义为一个域(段)，域和域之间使用分割符分割
- '/……/'：表示中间的是要匹配的正则表达式，省略号……表示上式中的正则表达式
- [0-9]：表示匹配0-9的数字
```Bash
awk '/^([0-9]{3}-|\([0-9]{3}\) )[0-9]{3}-[0-9]{4}$/' file.txt
```
0 ms, faster than 100.00% ; 3.3 MB, less than 10.71% 

#### Approach: using sed
- sed：一款流编辑工具，用来对文本进行过滤与替换工作，  sed通过输入读取文件内容，但**一次仅读取一行内容**进行某些指令处理后输出，sed更适合于处理大数据文件。
- -n：表示关闭默认输出，默认将自动打印所有行，这样就不会打印出不符合要求的数字串了
- -r：表示支持扩展正则+ ? () {} |。后面的正则表达式和上面都相同，就是后面多了一个p
- p：在用sed时，p和-n合用，表示打印某一行，这样才能把符合要求的行打印出来：
- [0-9]：表示匹配0-9的数字，也可以替换成：\d
```Bash
sed -n -r '/^([0-9]{3}-|\([0-9]{3}\) )[0-9]{3}-[0-9]{4}$/p' file.txt
```
4 ms, faster than 56.48%  ; 3.1 MB, less than 96.43%
