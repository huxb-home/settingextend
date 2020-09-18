# settingextend
灵感来源于公司的一个公共类库，想对这个进行重新设计。实现配置内容的引用，让配置更简单、灵活。经过处理后获得一串字符串，用于页面展示。或者获得一种数据类型（目前只有数组和字典），用于代码编写。

# 语法
将配置值划分为头部和配置两部分。头部是声明此配置的类型，目前有类型、引用共两种。<br/>
头部通过关键词来识别。
- #开头，表示注释，不会解析
- 空行，会被过滤
## 头部语法
### 类型
分为数组、字典和代码。语法简单，申明只有顶部一行。语法如下：<br/>
数组：
```
# 这是一个数组，解析对象中为字符串数组
type array

用户
管理员
编辑
```
字典：
```
# 这是一个字典，解析对象中键值均为字符串
type dictionary

user=用户
admin=管理员
editor=编辑
```
代码：
```
# 这是代码示例，解析对象中值为字符串。通过```print```函数输出，多个输出最后用换行符连接。
# 目前功能简陋，还不清晰用途。
# 语法与.NET语法保持一致。暂时不支持命名空间和类库引用，在代码文本混合类型中支持
type code

print("输出1");
print(DateTime.Now.ToString("yyyy-MM-dd"));
```
### 引用
此类输出对象值为字符串。设计用途为公共页面渲染。<br/>
注意：dll看起来不用引用，在当前目录下会识别。<br/>
语法如下：
```
import [path|dll|namespace] [路径|dll名称|命名空间] [变量名]
```
### 变量
会引起代码中变量冲突，暂时不实现。