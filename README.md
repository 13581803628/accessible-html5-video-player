<img src="images/logo_347x50_PPa11y.png" width="347" height="50" alt="PayPal accessibility logo" />

# 无障碍HTML5视频播放器

##由PayPal辅助功能团队研发
详情参考下面的 [作者](#作者) 部分。

## 这是什么？
一个轻量级的HTML5视频播放器，包括支持字幕和屏幕阅读器的辅助功能。有关详细信息，请在PayPal工程博客上阅读博文[无障碍HTML5视频播放器介绍](https://www.paypal-engineering.com/2014/09/05/introducing-an-accessible-html5-video-player/)。

## 特征
- 提供具有自定义控件的HTML5视频播放器。
- 支持字幕；简单地载入使用标准HTML5视频语法的VTT字幕文件。
- 使用本地HTML5形式的控件来控制音量（`range`类型的`<iput>`标签）和进度条（progress元素）。
- 适用于键盘用户和触幕用户。
- 默认设置字幕开启或关闭的选项（加载时）。
- 提供选项来设置回退和快进的秒数。
- 控件的文本字符串被扩展以允许标准化（2015年秋季标准）。
- 没有依赖库。使用 "vanilla" JavaScript 编写。
- 当JavaScript不可用时，将使用浏览器的本地控件。
## 实现

### CSS 和 图像
将CSS文件引入你的HTML页面的document文件头中。您还需要上传精灵图像（或使用自己的图像）并调整CSS文件中的路径。
```html
<link rel="stylesheet" href="/css/px-video.css" />
```

### HTML
在你的HTML5页面的document的文件体中插入视频标签（`<video>`）。替换视频，海报和标题url地址。根据需要修改视频和封面图像的大小。
```html
<div class="px-video-container" id="myvid">
	<div class="px-video-img-captions-container">
		<div class="px-video-captions hide" aria-hidden="true"></div>
		<video width="640" height="360" poster="media/foo.jpg" controls>
			<source src="foo.mp4" type="video/mp4" />
			<source src="foo.webm" type="video/webm" />
			<track kind="captions" label="English captions" src="media/foo.vtt" srclang="en" default />
			<div>
				<a href="foo.mp4">
					<img src="media/foo.jpg" width="640" height="360" alt="download video" />
				</a>
			</div>
		</video>
	</div>
	<div class="px-video-controls"></div>
</div>
```

### JavaScript
在你的HTML页面document文件体闭合之前（即，在`</body>`之前）引入两个JavaScript文件。添加一个Script标签元素来初始化视频，参数以JSON的形式传进去，参数有：

- videoId: 部件容器的ID值（字符串类型）[必须]
- captionsOnDefault: 表示加载时是否显示或隐藏字幕（布尔类型）[可选，默认值为true]
- seekInterval: 快进和回退的秒数（整数类型）[可选，默认值为10]
- videoTitle: 视频的简称；用于Play按钮上aria-label属性，向触屏用户阐明将要播放的内容（文本类型[可选，默认值为"Play"]
- debug: 打开或关闭控制台日志（布尔类型）[可选，默认值为false]

```html
<script src="js/strings.js"></script>
<script src="js/px-video.js"></script>
<script>
// 初始化
new InitPxVideo({
	"videoId": "myvid",
	"captionsOnDefault": true,
	"seekInterval": 20,
	"videoTitle": "clips of stand-up comedy",
	"debug": true
});
</script>
```

##在线演示
[查看演示](http://paypal.github.io/accessible-html5-video-player/)

## 反馈和贡献
如果您遇到任何错误，或者您有改进想法，请随时打开问题页面或发送pull请求。

您也可以通过Twitter联系PayPal辅助功能团队：[@PayPalInclusive](https://twitter.com/paypalinclusive)

## 作者
本项目的最初作者有：
- 丹尼斯·布里，主要开发者 || [https://github.com/weboverhauls](https://github.com/weboverhauls) || [@dennisl](https://twitter.com/dennisl)
- 维克托·萨拉伦，咨询和测试 || [https://github.com/vick08](https://github.com/vick08) || [@vick08](https://twitter.com/vick08)
- 杰森·加布里埃勒, 谘询专家
- 蒂姆·瑞修蒂克, 设计师

## 浏览器支持
- Chrome：完全支持。
- Safari：完全支持。
- Firefox：完全支持。
- Internet Explorer 10, 11：完全支持。
- Internet Explorer 9：使用本地视频播放器（美学选择，因为不支持HTML5`range`类型的`<iput>`标签和progress进度元素的审美选择）。
- Internet Explorer 8：渲染视频元素的后退内容（在演示中，这是与视频文件链接的图像）。
- 智能手机和平板电脑： 控件和字幕不是自定义的，因为在最新版本中都是本地支持的。

## 限制和已知问题
- 目前，每个视频只支持一个字幕文件。
- 只支持VTT字幕文件（不是SRT或TTML）。不支持VTT提示设置，而是内联样式功能（参见前几行的例子）。
- 控件的最小宽度为360px。

## 相关资源
- [HTML5视频事件和API](http://www.w3.org/2010/05/video/mediaevents.html) - 由W3C制作
- [在HTML5视频中添加字幕和字幕](https://developer.mozilla.org/en-US/Apps/Build/Audio_and_video_delivery/Adding_captions_and_subtitles_to_HTML5_video#Internet_Explorer) - 由MDN制作
- [简单的SubRip到WebVTT转换器](https://atelier.u-sub.net/srt2vtt/) - 将SRT字幕转换为WebVTT的工具
- [Able 播放器](https://github.com/ableplayer/ableplayer) - Terrill Thompson研发的可访问跨浏览器媒体播放器

### 受PayPal无障碍HTML5视频播放器影响的项目
- [通用视频播放器](https://source.ind.ie/project/video-player) - by Ind.ie, @LauraKalbag
- [Plyr](https://github.com/selz/plyr) - by @sam_potts, @selz

## 版权和许可证
Copyright 2014, PayPal under [the BSD license](LICENSE.md).

