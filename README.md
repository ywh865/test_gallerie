# hexo_gallerie使用
###### 注：项目测试阶段中
## 1、添加【相册】菜单
#### 这里要修改几个文件：
* 主题的配置文件_config.yml ，在menu下添加以下代码:
```
Galleries:
    url: /galleries
    icon: fa-photo
```
* 主题的语言配置文件目录 languages下的 default.yml和zh-CN.yml，分别是英文和中文的配置文件，分别添加：
```
galleries: galleries

galleries: 相册
```
* 主题目录下layout/_partial/navigation.ejs和layout/_partial/mobile-nav.ejs文件里添加
```
    menuMap.set("Galleries", "相册");
```
* 站点下添加galleries/index.html文件
在站点根目录source下新建galleries目录，然后在该目录下新建index.md，就会生成index.html文件了。

## 2、生成相册目录和相册列表
### hexo把文件当成一个普通的文章来渲染，需要自定义样式，让它渲染成普通的文章。让它渲染成一个layout,也就是我们自定义的模板。
##### 需要以下操作：
###### 在index.md文件里添加以下内容：
```
---
title: 相册
layout: "galleries"
---
```
###### 添加自定义CSS样式文件
+ 主题目录下的source/css里将gallery.css文件放进去
+ 主题layout目录下将galleries.ejs文件放进去
+ 主题layout目录下将gallery.ejs文件放进去

#### 以上实现的功能和引用插件：
1. 读取相册配置文件并把相册目录和相册列表都渲染成HTML
注：<% %>包起来的代码是ejs语法

2. 引用了两个jquery插件，分别是fancybox和justifiedGallery,
* 是点击弹出的轮播插件，
* 是自动调整图片布局的插件，
注：需要自行下载并放到相应目录

### 3、制作相册配置文件
在站点目录sources/_data/下放入galleries.json的文件，galleries.json文件需自行修改参数。

galleries.json文件为包含多个相册的列表JSON，相册各个字段含义：
* name 相册标题
* cover 封面图片
* description 相册介绍
* photos 图片列表

配置文件建好了之后还没完，在galleries下建立对应的相册名称目录和文件，然后下面再分别新建index.md文件，建好相应目录和文件之后，相册目录和列表就会正常渲染出来。

### 4、照片列表的布局选择
不同的图片有不同的宽高比，图片有两种显示方式，一是强制缩放到固定的宽高，二是裁切只显示一部分，但是都有缺点，第一个会图片会变形，第二个图片显示不全。

+ 瀑布流布局，
用CCS3的新特性实现的，这种模式的特点是等宽布局，固定列数，图片高度自适应

+ 等高布局
这种布局是等高布局，图片高度一致，宽度自适应，需要js动态设置图片的宽高来实现，需引用的justifiedGallery插件实现
下面代码的功能就是初始化这个插件，间距是5px，每一行的高度是150px。
```
  $("#mygallery").justifiedGallery({margins: 5, rowHeight: 150});
```

###### 注：两种布局代码中都有包含，可把上面那句代码注释掉就可以切换到瀑布流布局。
