---
layout: post
title: "备忘录——GitHub本地设置多账号SSH登陆"
date: 2016-12-17 14:56:21
categories: article
tags: log, tech, tips, tricks, 备忘录
---

关于标题
===

总感觉标题有语法问题，改不过来了。

前言
===

因为某些原因，需要在一台电脑上使用多个GitHub账号。原来参考某篇文章设置过，现在找不到那篇文章了(其实是我忘记怎么描述这个问题了，这也是我觉得本文标题有问题的原因:disappointed_relieved:)，本文权作记录。

重点在第4步第5步。

正文
===

1. 注册GitHub账号

    本文假设GitHub账号为sampleaccount

2. 本地生成SSH key

    这里可以参考GitHub提供的**[这篇教程][1]{:target="_blank"}**

        $ ssh-keygen

        Enter a file in which to save the key (/Users/you/.ssh/id_rsa):
        #本文假设密钥文件名为id_rsa_sampleaccount

3. 在GitHub设置页面添加公钥

    将公钥内容复制到剪贴板:

        $ pbcopy < ~/.ssh/id_rsa_sampleaccount.pub

    在**[这个页面][2]{:target="_blank"}**点击**New SSH key**按钮，粘贴刚才复制的公钥内容。

4. **本地config文件设置**

    编辑.ssh/config文件，为每个GitHub账号添加如下内容：

        Host github-sampleaccount
            HostName github.com
            User git
            IdentityFile ~/.ssh/id_rsa_sampleaccount

5. **操作git库**

    获取代码:

        git clone git@github.com:merlinz-test/merlinz-test.github.io.git

    这样做会报错，需要把github.com换成我们config文件中的**Host字段**，即github-sampleaccount

        git clone git@github-sampleaccount:merlinz-test/merlinz-test.github.io.git

    其他git操作如常。


参考
===

参考上文前言部分。



[1]: https://help.github.com/articles/generating-an-ssh-key/
[2]: https://github.com/settings/keys
