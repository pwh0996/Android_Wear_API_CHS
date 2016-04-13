Android Wear API 中文翻译
=============================================

[英文原版](https://developer.android.com/training/building-wearables.html)

> 于本人最近学习Android Wear开发,顺便翻译一下开发文档。可能有很多不对的地方。
欢迎大家更正！有兴趣翻译的同学可以加我QQ：279291014

---

# 当前阶段

###[翻译目录][1]

# 译者记录

* 创建Android Wear Apps
    * 创建并运行Android Wear App
    * 创建自定义通知
    * 添加语音功能
    * 打包Android Wear应用
    * 通过蓝牙调试

* 创建自定义UIs
    * 定义布局
    * 创建卡片
    * 创建列表1.0
    * 创建列表1.1
    * 创建2D_Picker
    * 显示确认
    * 退出全屏界面

* 添加Android Wear通知
    * 创建通知
    * 在通知中接收语音输入
    * 给通知添加页面
    * 叠加通知

* 发送和同步数据
    * 访问数据层
    * 同步数据项
    * 传输资源
    * 发送和接收消息
    * 处理数据层事件

* 创建表盘 
    * 设计表盘 
    * 构建表盘Service
    * 绘制表盘
    * 在表盘显示信息
    * 提供配置项Activities
    * 解决常见问题
    * 优化性能和电池续航
    * 获取地理位置

# 贡献力量

如果想做出贡献的话，你可以：

- 帮忙翻译
- 帮忙校对，挑错别字、病句等等
- 提出修改建议
- 提出术语翻译建议

# 翻译建议

如果你愿意一起校对的话，请仔细阅读：

- 使用markdown进行翻译，文件名必须使用英文，因为中文的话gitbook编译的时候会出问题

# 关于术语

翻译术语的时候请参考这个流程：

- 尽量保证和已翻译的内容一致
- 尽量先搜索，一般来说编程语言的大部分术语是一样的，可以参考[微软官方术语搜索](http://www.microsoft.com/Language/zh-cn/Search.aspx)
- 如果以上两条都没有找到合适的结果，请自己决定一个合适的翻译或者直接使用英文原文，后期校对的时候会进行统一

# 参考流程

有些朋友可能不太清楚如何帮忙翻译，我这里写一个简单的流程，大家可以参考一下：

1. 首先fork我的项目
2. 把fork过去的项目也就是你的项目clone到你的本地
3. 在命令行运行 `git branch develop` 来创建一个新分支
4. 运行 `git checkout develop` 来切换到新分支
5. 运行 `git remote add upstream https://github.com/pwh0996/Android_Wear_API_CHS.git` 把我的库添加为远端库
6. 运行 `git remote update`更新
7. 运行 `git fetch upstream gh-pages` 拉取我的库的更新到本地
8. 运行 `git rebase upstream/gh-pages` 将我的更新合并到你的分支

这是一个初始化流程，只需要做一遍就行，之后请一直在develop分支进行修改。

如果修改过程中我的库有了更新，请重复6、7、8步。

修改之后，首先push到你的库，然后登录GitHub，在你的库的首页可以看到一个 `pull request` 按钮，点击它，填写一些说明信息，然后提交即可。


# 开源协议
基于[WTFPL](http://en.wikipedia.org/wiki/WTFPL)协议开源。


  [1]: https://github.com/pwh0996/Android_Wear_API_CHS/blob/master/Building_Apps_for_Wearables/index.md