# MarkDown

[toc]

## 多文件跳转章节的坑

多文件跳转至指定章节markDown 语法支持如下： 

```
文件 a
[jump](./b.md##Chapter2)

文件 b
# Chapter1
## Chapter2
```

但是经测试，实际跳转效果和解析器有关 ，目前发现typora 不支持跨文件跳转； IDEA 支持跨文件，不支持跨文件至对应标题； 只有github 是完美支持跳转语法的 。 **因此，凡是涉及跨文件跳转的超链接， 用typora 预览的markDown，只能手动根据标签地址来路由了。**

![image-20221021152512588](https://raw.githubusercontent.com/Assassin-King/Typora-Note/master/Images/markdown/image-20221021152512588.png)

![image-20221021152601286](https://raw.githubusercontent.com/Assassin-King/Typora-Note/master/Images/markdown/image-20221021152601286.png)





![image-20221021152626512](https://raw.githubusercontent.com/Assassin-King/Typora-Note/master/Images/markdown/image-20221021152626512.png)