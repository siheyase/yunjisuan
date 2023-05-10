---
title: "Jekyll gitPage 静态网站搭建过程的记录"
categories:
  - blog
tags:
  - Jekyll
  - Homework
---

## 云计算Lab9  

>实验内容   

部署一个静态网页博客。  
选择一个自己感兴趣或擅长的主题来制作一个静态网页博客，比如个人介绍、爱好分享、技术总结等。  
设计至少四个页面来展示博客内容，不限于首页、关于我、文章列表、文章详情等。 

>作业提交   

你需要在指定 issue 中给出博客链接，并附上自己对本次作业的总结或反思（可以把这部分内容放在博客页面中，给出对应链接即可）。  
  
**思路**：先在本地编写符合Jekyll规范的网站源码，然后上传到github，由github生成并托管整个网站。  
后来发现如果只是作业的话直接在GitHub上修改就行，很方便。。。  

>过程记录  

每次部署成功的actions页面应该是如下图所示：  
![]({{ "/assets/images/success.png" | prepend :site.baseurl}})

### 显示图片  
**问题**：md文件中的图片无法在网站上显示。  
正常的md文件，显示图片的路径是`![](path)`，但是这样我在查看github上的markdown文件时可以看到图片，但是打开静态网站，怎么也加载不出来图片。  
**解决**：搜索发现，是因为Jekyll 会按照 liquid 语法进行解析md文件，所以预览能看到网站上看不到。  
正确的添加图片的语法是：  

![]({{ "/assets/images/1.png" | prepend :site.baseurl}})

### 在md转化的post中插入可以在线播放视频  
第一种 使用样式代码插入iframe  

```html
<div class="video-container" style="
    position: relative;
    padding-bottom:56.25%;
    padding-top:30px;
    height:0;
    overflow:hidden;
">
<iframe
  src="https://www.youtube.com/embed/ZYjYAT2g-1Q" # vedio path
  width="560"
  height="315"
  frameborder="0"
  allowfullscreen=""
  style="
    position: absolute;
    top:0;
    left:0;
    width:100%;
    height:100%;
">
</iframe>
</div>
```
成功的效果如[post_vedio][p1]所示  

第二种，因为每次都插入这段代码很麻烦。Jekyll可以使用include标签来引入位于_includes文件夹里面的html片段，并且可以在include标签传入变量，在html模板中进行处理生成html片段。  
创建_include目录  
在其中添加iframe.html文件  
在md文件中可以使用liquid对应的的格式插入视频    

![]({{ "/assets/images/2.png" | prepend :site.baseurl}})
这一行一开始在Build Jekyll中报错（查看actions）。  
![]({{ "/assets/images/3.png" | prepend :site.baseurl}})  
![]({{ "/assets/images/4.png" | prepend :site.baseurl}})
我发现我在md文件中直接写这行，无论我用什么符号修饰，依旧会被识别，说明jekyll对于md的所有内容都会进行liquid语法的解析。因此我只能改为插入图片。。。

效果如[post-vedio2][p2]所示  

>更改_config.yml文件修改配置  

**更新网站徽标:**logo: "/assets/images/88x88.png"
{: .notice--info}

**更新皮肤主题:**minimal_mistakes_skin: "sunrise" # default
{: .notice--info}

[p1]:https://siheyase.github.io/yunjisuan/blog/post-vedio
[p2]:https://siheyase.github.io/yunjisuan/blog/post-vedio2
