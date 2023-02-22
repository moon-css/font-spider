# 字蛛

## 目的
分析本地*CSS*和*HTML文件*获取`WebFont`中没有使用的字符，通过删除这些字符实现字体库文件的压缩，并生成可以跨浏览器使用的文件格式，从而解决加载缓慢的问题。

## 下载和安装

### 通过node工具导入字蛛

- 全局导入
```
npm install font-spider -g
```
在命令窗口中输入指令，下载字蛛并全局安装

- 检查版本
```
font-spider  -V
```
运行本行指令可查看字蛛有无安装成功，并获得使用版本，结果如下即为安装成功。

<img width="589" alt="image" src="https://user-images.githubusercontent.com/70060430/220540441-02abc93d-d235-49c8-b616-ebf6fb0136db.png">



## 使用

- 在*css*中使用`WebFont`:
```css
/*声明WebFont,font-family为自定义字体库命名，src中的文件名随着使用的ttf文件名称的不同而改变*/
@font-face{
    font-family:'fontName';
    src:url('../font/FZYANSJW_CU.eot');
    src:
        url('../font/FZYANSJW_CU.eot?#font-spider') format('embedded-opentype'),
        url('../font/FZYANSJW_CU.woff2') format('woff2'),
        url('../font/FZYANSJW_CU.woff') format('woff'),
        url('../font/FZYANSJW_CU.ttf') format('truetype'),
        url('../font/FZYANSJW_CU.svg') format('svg');
    font-weight: normal;
    font-size: normal;
}

/*指定字体*/
#test{
    font-family:'fontName';
}

```
*注意事项：`@font-face`的`src`定义的字体库路径中的.ttf文件必须存在，其余格式文件由字蛛工具自动生成*

- 运行`font-spider`命令
```
 font-spider index.html
```

## 测试用例
1. [index.html](https://github.com/moon-css/font-spider/blob/main/index.html)

如图所示，`div`标签中放入项目中需要使用指定样式的**所有字符**（中文，英文，标点符号等），且在本地运行时，使用**相对路径**的*css文件*。

<img width="895" alt="image" src="https://user-images.githubusercontent.com/70060430/220542073-3272eb98-8f97-4f22-a5be-bec686134f1f.png">

2. [style.css](https://github.com/moon-css/font-spider/blob/main/css/style.css)

在*css*中使用`WebFont`引入指定字体库，此处也使用**相对路径**，并且注意*.ttf*文件一定要存在。同时使用*css选择器*将`div`的字体样式指定为我们命名的`fontName`。

<img width="903" alt="image" src="https://user-images.githubusercontent.com/70060430/220542867-134c6025-5195-4453-a005-162ab661f1ac.png">

3.压缩打包

将以上1，2两点都处理好之后，执行打包命令，如下图：

<img width="644" alt="image" src="https://user-images.githubusercontent.com/70060430/220545854-7a55105a-0013-459a-a6b8-b5518502bc3e.png">

结果如图所示即为打包成功，此时*font*文件夹中会将初始字体库文件放入*.font-spider*隐藏文件中，并重新压缩打包生成新的字体库文件，如下图：

<img width="357" alt="image" src="https://user-images.githubusercontent.com/70060430/220548361-99510425-c175-412d-acbf-c9be7d68c796.png">

如果出现报错，可以检查以下两点：
- 是否使用了两次`@font-face`
- *.ttf*文件路径有没有出错，文件是否存在



## 注意点总结
### 开发时
1. 运行打包命令之前一定要将所有需要使用自定义文字库的字符放入*html*文件；
2. 使用相对路径的*css*和*webfont*；
3. 每次有新增加的文字或字符时，需要将font文件夹的*.ttf*文件更换为之前的初始字体库文件，再运行打包命令。

### 上线时
上线项目时，不需要使用以上的代码，只需要使用*font*文件夹中压缩之后的字体库文件，通过`font-family:fontName;`指定字体样式名就可以正常使用
