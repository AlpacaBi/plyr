[English](readme.md) | [中文文档](readme_zh.md)

Plyr是一个简单、轻量、开放和可定制化的Html5、Youtube和Vimeo媒体播放器，支持[现代](#浏览器兼容性)浏览器。


[查看在线demo](https://plyr.io) - [捐献](#捐献) - [Slack](https://bit.ly/plyr-chat) - [![npm version](https://badge.fury.io/js/plyr.svg)](https://badge.fury.io/js/plyr)

[![Image of Plyr](https://cdn.plyr.io/static/demo/screenshot.png?v=3)](https://plyr.io)

# 功能特性

-   📼 **HTML视频 & 音频, YouTube & Vimeo** - 支持主流视频格式
-   💪 **开放性** - 支持VTT字幕和屏幕阅读器
-   🔧 **[可定制化](#html)** - 你可以根据自己的需求通过HTML标记来定制播放器
-   😎 **HTML语义化** - 使用 _语义化_ 的元素标签. 使用`<input type="range">` 标签生成音量滑动控制条和使用 `<progress>`标签来生成进度条, `<button>`标签用来生成按钮. 我们不会使用
    `<span>` 或者 `<a href="#">` 来生成一个按钮
-   📱 **响应式** - 可以在任何尺寸的屏幕设备正常工作
-   💵 **[商业化](#广告支持（Ads）)** - 你可以给你的视频插入广告盈利
-   📹 **[流媒体](#demos)** - 支持hls.js、shaka和dash.js流媒体播放
-   🎛 **[API](#api)** - 提供了切换播放、音量、搜索等API
-   🎤 **[事件](#events)** - 不受Vimeo和YouTube API的干扰, 所有事件都是跨格式标准化的
-   🔎 **[全屏](#全屏)** - 支持本机原生全屏，并可回退到“全窗口”模式
-   ⌨️ **[快捷键](#键盘快捷键)** - 支持键盘快捷键
-   🖥 **画中画模式** - 支持画中画模式
-   📱 **Playsinline属性** - 支持 `playsinline` 属性
-   🏎 **播放速度控制** - 可以调整视频播放速度
-   📖 **多重字幕** - 支持多重字幕轨
-   🌎 **i18n支持** - 支持国际化，多国语言支持
-   👌 **[预览缩略图](#预览缩略图)** - 支持显示预览缩略图
-   🤟 **无框架依赖** - 用原生es6编写，不依赖jquery
-   💁‍♀️ **SASS** - 已包含在项目生成过程中

### Demos

你可以在Codepen中体验Plyr: [HTML5视频](https://codepen.io/pen?template=bKeqpr), [HTML5音频](https://codepen.io/pen?template=rKLywR), [YouTube](https://codepen.io/pen?template=GGqbbJ), [Vimeo](https://codepen.io/pen?template=bKeXNq). 当然我们也提供了流媒体版本: [Dash.js](https://codepen.io/pen?template=zaBgBy), [Hls.js](https://codepen.io/pen?template=oyLKQb) 和 [Shaka Player](https://codepen.io/pen?template=ZRpzZO)

# 快速开始

## HTML

Plyr扩展了标准的[HTML5媒体元素](https://developer.mozilla.org/en-US/docs/Web/API/HTMLMediaElement)

### HTML5视频

```html
<video poster="/path/to/poster.jpg" id="player" playsinline controls>
    <source src="/path/to/video.mp4" type="video/mp4" />
    <source src="/path/to/video.webm" type="video/webm" />

    <!-- Captions are optional -->
    <track kind="captions" label="English captions" src="/path/to/captions.vtt" srclang="en" default />
</video>
```

### HTML5音频

```html
<audio id="player" controls>
    <source src="/path/to/audio.mp3" type="audio/mp3" />
    <source src="/path/to/audio.ogg" type="audio/ogg" />
</audio>
```

对于YouTube和Vimeo播放器，Plyr默认以渐进式增强的方式使用嵌入式的`<iframe>`。举个例子，设置`plyr_uu video-embed`类名将使Plyr的响应式配置生效。您可以将autoplay、loop、hl（仅限YouTube）和playsinline（仅限YouTube）查询参数添加到url，它们将自动设置为配置选项。对于YouTube，应该更新源代码以作用在您托管嵌入的域名，或者您可以选择忽略它。

### YouTube

我们建议以[渐进式增强](https://www.smashingmagazine.com/2009/04/progressive-enhancement-what-it-is-and-how-to-use-it/)的方式使用嵌入式播放器。您可以选择使用`<iframe>` 作为源元素（Plyr进行渐进式增强的地方）。或者使用普通的标准`<div>`，只不过要带上带两个基本数据属性 `data-plyr-provider`和 `data-plyr-embed-id`。


```html
<div class="plyr__video-embed" id="player">
    <iframe
        src="https://www.youtube.com/embed/bTqVqk7FSmY?origin=https://plyr.io&amp;iv_load_policy=3&amp;modestbranding=1&amp;playsinline=1&amp;showinfo=0&amp;rel=0&amp;enablejsapi=1"
        allowfullscreen
        allowtransparency
        allow="autoplay"
    ></iframe>
</div>
```

_注意_: `plyr__video-embed`类名会使播放器成为16:9响应式（最常见播放器比例）的`iframe`嵌入式播放器。当Plyr播放器本身启动时，将使用自定义的“ratio”配置选项。

或者在`<div>`里使用非渐进增强的方式：

```html
<div id="player" data-plyr-provider="youtube" data-plyr-embed-id="bTqVqk7FSmY"></div>
```

_注意_: `data-plyr-embed-id` 既可以是video ID，也可以是该媒体的URL地址。

### Vimeo

和上面的youtube差不多

```html
<div class="plyr__video-embed" id="player">
    <iframe
        src="https://player.vimeo.com/video/76979871?loop=false&amp;byline=false&amp;portrait=false&amp;title=false&amp;speed=true&amp;transparent=0&amp;gesture=media"
        allowfullscreen
        allowtransparency
        allow="autoplay"
    ></iframe>
</div>
```

或者在`<div>`里使用非渐进增强的方式：

```html
<div id="player" data-plyr-provider="vimeo" data-plyr-embed-id="76979871"></div>
```

## JavaScript

你可以用ES6的模块功能加载Plyr:

```javascript
import Plyr from 'plyr';

const player = new Plyr('#player');
```

当然了，你也可以在`</body>` 标签前面直接引入`plyr.js`脚本，然后在js中创建Plyr的新实例，如下所示

```html
<script src="path/to/plyr.js"></script>
<script>
    const player = new Plyr('#player');
</script>
```

你可以在文档的 [初始化](#初始化) 部分查看高级设置的详细信息

你也可以使用CDN外链(由[Fastly](https://www.fastly.com/)提供) 来引入JavaScript部分. 这里有两个版本; 一个是不包含[polyfills](#polyfills)的，另一个是包含的. 经过我本人测试，不包含[polyfills](#polyfills)不能兼容ie浏览器，而包含[polyfills](#polyfills)的则支持ie9以上的浏览器，只是体积会大一点。

```html
<script src="https://cdn.plyr.io/3.5.6/plyr.js"></script>
```

...或者带[polyfills](#polyfills)的（如果你的项目需要兼容ie浏览器，用这个）...

```html
<script src="https://cdn.plyr.io/3.5.6/plyr.polyfilled.js"></script>
```

## CSS

你可以在你页面的`<head>`直接引入 `plyr.css` 文件。

```html
<link rel="stylesheet" href="path/to/plyr.css" />
```

如果你想使用CDN外链(由[Fastly](https://www.fastly.com/)提供) 引入, 你可以直接复制下面的链接:

```html
<link rel="stylesheet" href="https://cdn.plyr.io/3.5.6/plyr.css" />
```

## SVG雪碧图

SVG雪碧图是从我们的CDN(由[Fastly](https://www.fastly.com/)提供)自动加载的。要更改此设置，请参见下面的选项。作为参考，可以在https://cdn.plyr.io/3.5.6/plyr.svg 上找到承载cdn的SVG雪碧图。

# 广告支持（Ads）

Plyr 与 [vi.ai](https://vi.ai/publisher-video-monetization/?aid=plyrio) 广告商合作，为你的视频提供了商业化选择. 操作起来很容易:

-   [注册一个 vi.ai 账户](https://vi.ai/publisher-video-monetization/?aid=plyrio)
-   获取您的publisher ID
-   在[config options](#options) 配置中开启广告选项，并输入你的publisher ID

有关广告的任何问题都可以跟vi.ai反映，如果广告功能在Plyr出现问题你可以提issue。

# 高级配置

## SASS

你可以让`bundle.scss`包含进`/src`里面作为项目打包构建（build）的一部分，并且根据你的设计修改各种变量。Sass要求你使用`autoprefixer`（您应该已经在使用了！），因为所有声明都使用w3c标准。 

Plyr的HTML标签使用BEM方法（一种命名规范）命名， 例如`.plyr__controls`。您可以更改`option`中的class hooks,以匹配任何你自己写的自定义CSS。你可以查看javascript源代码了解更多信息。

## SVG

Plyr控件中使用的图标加载在SVG雪碧图中。默认情况下，雪碧图会自动从CDN加载。如果你在自己项目中已经有一个自己的图标，您可以包含源plyr图标（请参见`/src/sprite`了解源图标）。


### 使用`iconUrl`配置

你可以配置自己的`iconUrl`参数，Plyr将判断：
- url是否是绝对的
- 由于当前浏览器的原因，ajax/cors请求加载的限制
- 如果是相对路径，直接使用路径

如果你在自己的站点使用了`<base>`标签，你可能要去使用[svgfixer.js](https://gist.github.com/leonderijke/c5cf7c5b2e424c0061d2)

你可以从这里查到更多关于SVG雪碧图的详细资料：[http://css-tricks.com/svg-sprites-use-better-icon-fonts/](http://css-tricks.com/svg-sprites-use-better-icon-fonts/)

或者是AJAX技术相关资料：[http://css-tricks.com/ajaxing-svg-sprite/](http://css-tricks.com/ajaxing-svg-sprite/)

## 跨域 (CORS)

您应该会注意到示例demo的`<video>`元素带`crossorigin`属性。这是因为我们的字幕文件是从别的域名加载过来的，如果你的字幕文件也是托管在别的域名上，你就必须添加`crossorigin`属性并且在相应的域名的后台服务器配置好了CORS头设置。关于更多CORS信息你可以查看MDN文档：[https://developer.mozilla.org/en-US/docs/Web/HTTP/Access_control_CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/Access_control_CORS)

## 字幕（Captions）

支持在线字幕文件加载。如果要添加字幕轨，请查看上面的HTML示例的`<track>`元素。当然了要确保[验证你的字幕文件](https://quuz.org/webvtt/)。

## JavaScript

### 初始化

You can specify a range of arguments for the constructor to use:

-   [CSS选择器](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors)
-   [`HTMLElement`](https://developer.mozilla.org/en/docs/Web/API/HTMLElement)
-   一个 [jQuery](https://jquery.com) 对象

_注意_: If a `NodeList`, `Array`, or jQuery object are passed, the first element will be used for setup. To setup multiple players, see [multiple players](#multiple-players) below.

#### 单播放器

通过CSS选择器（必须兼容[`querySelector`](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelector)）:

```javascript
const player = new Plyr('#player');
```

通过 [HTMLElement](https://developer.mozilla.org/en/docs/Web/API/HTMLElement):

```javascript
const player = new Plyr(document.getElementById('player'));
```

```javascript
const player = new Plyr(document.querySelector('.js-player'));
```

The HTMLElement or string selector can be the target `<video>`, `<audio>`, or `<div>` wrapper for embeds.

#### Multiple players

在这里你有两个选择. You can either use a simple array loop to map the constructor:

```javascript
const players = Array.from(document.querySelectorAll('.js-player')).map(p => new Plyr(p));
```

...or use a static method where you can pass a [CSS string selector](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors), a [NodeList](https://developer.mozilla.org/en-US/docs/Web/API/NodeList), an [Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array) of [HTMLElement](https://developer.mozilla.org/en/docs/Web/API/HTMLElement), or a [JQuery](https://jquery.com) object:

```javascript
const players = Plyr.setup('.js-player');
```

Both options will also return an array of instances in the order of they were in the DOM for the string selector or the source NodeList or Array.

#### Options

构造函数的第二个参数是[options](#options)对象：

```javascript
const player = new Plyr('#player', {
    title: 'Example Title',
});
```
Options可以作为对象传递给上述的构造函数，或者在每个目标元素的`data-plyr-config` 属性中作为JSON传递：


```html
<video src="/path/to/video.mp4" id="player" controls data-plyr-config='{ "title": "Example Title" }'></video>
```
注意，object keys上的单引号封装了json和双引号。只有字符串值需要双引号。


| 配置项               | 类型                       | 默认值                                                                                                                        | 说明                                                                                                                                                                                                                                                                                                                                                                                             |
| -------------------- | -------------------------- | ------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `enabled`            | Boolean                    | `true`                                                                                                                         | 完全禁用Plyr。这将允许您执行UA检查，或类似于为某个UA启用或禁用Plyr（UA:浏览器标识,可以使得服务器能够识别客户使用的操作系统及版本）。如下面的例子。                                                                                                                                                                                                                           |
| `debug`              | Boolean                    | `false`                                                                                                                        | 在控制台中显示调试信息                                                                                                                                                                                                                                                                                                                                                            |
| `controls`           | Array, Function 或者 Element | `['play-large', 'play', 'progress', 'current-time', 'mute', 'volume', 'captions', 'settings', 'pip', 'airplay', 'fullscreen']` | If a function is passed, it is assumed your method will return either an element or HTML string for the controls. Three arguments will be passed to your function; `id` (the unique id for the player), `seektime` (the seektime step in seconds), and `title` (the media title). See [controls.md](controls.md) for more info on how the html needs to be structured.                                  |
| `settings`           | Array                      | `['captions', 'quality', 'speed', 'loop']`                                                                                     | 如果使用的是默认控件，则可以指定要在菜单中显示的设置                                                                                                                                                                                                                                                                                                   |
| `i18n`               | Object                     | 查看 [defaults.js](/src/js/config/defaults.js)                                                                                  | 用于UI组件中文本的国际化多语言配置                                                                                                                                                                                                                                                                                                                                         |
| `loadSprite`         | Boolean                    | `true`                                                                                                                         | 加载指定为`iconUrl`选项的SVG雪碧图（如果是URL）. 如果为 `false`, 那就认定你是在自己加载雪碧图。                                                                                                                                                                                                                                                            |
| `iconUrl`            | String                     | `null`                                                                                                                         | 指定SVG雪碧图的URL或路径. 查看文档中 [SVG部分](#svg) 获取更多信息.                                                                                                                                                                                                                                                                                                                     |
| `iconPrefix`         | String                     | `plyr`                                                                                                                         | Specify the id prefix for the icons used in the default controls (e.g. "plyr-play" would be "plyr"). This is to prevent clashes if you're using your own SVG sprite but with the default controls. Most people can ignore this option.                                                                                                                                                                  |
| `blankVideo`         | String                     | `https://cdn.plyr.io/static/blank.mp4`                                                                                         | Specify a URL or path to a blank video file used to properly cancel network requests.                                                                                                                                                                                                                                                                                                                   |
| `autoplay`&sup2;     | Boolean                    | `false`                                                                                                                        | Autoplay the media on load. If the `autoplay` attribute is present on a `<video>` or `<audio>` element, this will be automatically set to true.                                                                                                                                                                                                                                                         |
| `autopause`&sup1;    | Boolean                    | `true`                                                                                                                         | Only allow one player playing at once.                                                                                                                                                                                                                                                                                                                                                                  |
| `seekTime`           | Number                     | `10`                                                                                                                           | The time, in seconds, to seek when a user hits fast forward or rewind.                                                                                                                                                                                                                                                                                                                                  |
| `volume`             | Number                     | `1`                                                                                                                            | 一个介于0到1的数字, 代表播放器的初始音量.                                                                                                                                                                                                                                                                                                                               |
| `muted`              | Boolean                    | `false`                                                                                                                        | Whether to start playback muted. If the `muted` attribute is present on a `<video>` or `<audio>` element, this will be automatically set to true.                                                                                                                                                                                                                                                       |
| `clickToPlay`        | Boolean                    | `true`                                                                                                                         | Click (or tap) of the video container will toggle play/pause.                                                                                                                                                                                                                                                                                                                                           |
| `disableContextMenu` | Boolean                    | `true`                                                                                                                         | Disable right click menu on video to <em>help</em> as very primitive obfuscation to prevent downloads of content.                                                                                                                                                                                                                                                                                       |
| `hideControls`       | Boolean                    | `true`                                                                                                                         | Hide video controls automatically after 2s of no mouse or focus movement, on control element blur (tab out), on playback start or entering fullscreen. As soon as the mouse is moved, a control element is focused or playback is paused, the controls reappear instantly.                                                                                                                              |
| `resetOnEnd`         | Boolean                    | false                                                                                                                          | Reset the playback to the start once playback is complete.                                                                                                                                                                                                                                                                                                                                              |
| `keyboard`           | Object                     | `{ focused: true, global: false }`                                                                                             | Enable [keyboard shortcuts](#shortcuts) for focused players only or globally                                                                                                                                                                                                                                                                                                                            |
| `tooltips`           | Object                     | `{ controls: false, seek: true }`                                                                                              | `controls`: Display control labels as tooltips on `:hover` & `:focus` (by default, the labels are screen reader only). `seek`: Display a seek tooltip to indicate on click where the media would seek to.                                                                                                                                                                                               |
| `duration`           | Number                     | `null`                                                                                                                         | Specify a custom duration for media.                                                                                                                                                                                                                                                                                                                                                                    |
| `displayDuration`    | Boolean                    | `true`                                                                                                                         | Displays the duration of the media on the "metadataloaded" event (on startup) in the current time display. This will only work if the `preload` attribute is not set to `none` (or is not set at all) and you choose not to display the duration (see `controls` option).                                                                                                                               |
| `invertTime`         | Boolean                    | `true`                                                                                                                         | Display the current time as a countdown rather than an incremental counter.                                                                                                                                                                                                                                                                                                                             |
| `toggleInvert`       | Boolean                    | `true`                                                                                                                         | Allow users to click to toggle the above.                                                                                                                                                                                                                                                                                                                                                               |
| `listeners`          | Object                     | `null`                                                                                                                         | Allows binding of event listeners to the controls before the default handlers. See the `defaults.js` for available listeners. If your handler prevents default on the event (`event.preventDefault()`), the default handler will not fire.                                                                                                                                                              |
| `captions`           | Object                     | `{ active: false, language: 'auto', update: false }`                                                                           | `active`: Toggles if captions should be active by default. `language`: Sets the default language to load (if available). 'auto' uses the browser language. `update`: Listen to changes to tracks and update menu. This is needed for some streaming libraries, but can result in unselectable language options).                                                                                        |
| `fullscreen`         | Object                     | `{ enabled: true, fallback: true, iosNative: false }`                                                                          | `enabled`: Toggles whether fullscreen should be enabled. `fallback`: Allow fallback to a full-window solution (`true`/`false`/`'force'`). `iosNative`: whether to use native iOS fullscreen when entering fullscreen (no custom controls)                                                                                                                                                               |
| `ratio`              | String                     | `null`                                                                                                                         | Force an aspect ratio for all videos. The format is `'w:h'` - e.g. `'16:9'` or `'4:3'`. If this is not specified then the default for HTML5 and Vimeo is to use the native resolution of the video. As dimensions are not available from YouTube via SDK, 16:9 is forced as a sensible default.                                                                                                         |
| `storage`            | Object                     | `{ enabled: true, key: 'plyr' }`                                                                                               | `enabled`: Allow use of local storage to store user settings. `key`: The key name to use.                                                                                                                                                                                                                                                                                                               |
| `speed`              | Object                     | `{ selected: 1, options: [0.5, 0.75, 1, 1.25, 1.5, 1.75, 2] }`                                                                 | `selected`: The default speed for playback. `options`: Options to display in the menu. Most browsers will refuse to play slower than 0.5.                                                                                                                                                                                                                                                               |
| `quality`            | Object                     | `{ default: 576, options: [4320, 2880, 2160, 1440, 1080, 720, 576, 480, 360, 240] }`                                           | `default` is the default quality level (if it exists in your sources). `options` are the options to display. This is used to filter the available sources.                                                                                                                                                                                                                                              |
| `loop`               | Object                     | `{ active: false }`                                                                                                            | `active`: Whether to loop the current video. If the `loop` attribute is present on a `<video>` or `<audio>` element, this will be automatically set to true This is an object to support future functionality.                                                                                                                                                                                          |
| `ads`                | Object                     | `{ enabled: false, publisherId: '' }`                                                                                          | `enabled`: Whether to enable advertisements. `publisherId`: Your unique [vi.ai](https://vi.ai/publisher-video-monetization/?aid=plyrio) publisher ID.                                                                                                                                                                                                                                                   |
| `urls`               | Object                     | See source.                                                                                                                    | If you wish to override any API URLs then you can do so here. You can also set a custom download URL for the download button.                                                                                                                                                                                                                                                                           |
| `vimeo`              | Object                     | `{ byline: false, portrait: false, title: false, speed: true, transparent: false }`                                            | See [Vimeo embed options](https://github.com/vimeo/player.js/#embed-options). Some are set automatically based on other config options, namely: `loop`, `autoplay`, `muted`, `gesture`, `playsinline`                                                                                                                                                                                                   |
| `youtube`            | Object                     | `{ noCookie: false, rel: 0, showinfo: 0, iv_load_policy: 3, modestbranding: 1 }`                                               | See [YouTube embed options](https://developers.google.com/youtube/player_parameters#Parameters). The only custom option is `noCookie` to use an alternative to YouTube that doesn't use cookies (useful for GDPR, etc). Some are set automatically based on other config options, namely: `autoplay`, `hl`, `controls`, `disablekb`, `playsinline`, `cc_load_policy`, `cc_lang_pref`, `widget_referrer` |
| `previewThumbnails`  | Object                     | `{ enabled: false, src: '' }`                                                                                                  | `enabled`: Whether to enable the preview thumbnails (they must be generated by you). `src` must be either a string or an array of strings representing URLs for the VTT files containing the image URL(s). Learn more about [preview thumbnails](#preview-thumbnails) below.                                                                                                                            |

1.  仅Vimeo
2.  通常不建议使用自动播放（autoplay）配置，因为它被视为一种负面的用户体验，它在许多浏览器中也被禁用。在提出Issues之前，先做功课。更多信息请访问：

-   https://webkit.org/blog/6784/new-video-policies-for-ios/
-   https://developers.google.com/web/updates/2017/09/autoplay-policy-changes
-   https://hacks.mozilla.org/2019/02/firefox-66-to-block-automatically-playing-audible-video-and-audio/

# API

下面是Plyr对象上的方法、setter和getter


## 对象（Object）

访问Plyr对象的最简单的方法，是通过构造函数创建Plyr实例，并赋给一个变量，如下：

```javascript
const player = new Plyr('#player', {
    /* options */
});
```

你也可以通过一些事件去访问对象:

```javascript
element.addEventListener('ready', event => {
    const player = event.detail.plyr;
});
```

## 方法（Methods）

示例方法:

```javascript
player.play(); // Start playback
player.fullscreen.enter(); // Enter fullscreen
```

| 方法                      | 参数             | 说明                                                                                               |
| ------------------------ | ---------------- | ---------------------------------------------------------------------------------------------------------- |
| `play()`&sup1;           | -                | 开始播放.                                                                                            |
| `pause()`                | -                | 暂停播放.                                                                                            |
| `togglePlay(toggle)`     | Boolean          | 切换播放暂停状态，如果没有参数，它将根据当前播放暂停状态切换。                      |
| `stop()`                 | -                | 停止播放并重置为开始。                                                                          |
| `restart()`              | -                | 重新播放.                                                                                                   |
| `rewind(seekTime)`       | Number           | Rewind playback by the specified seek time. If no parameter is passed, the default seek time will be used. |
| `forward(seekTime)`      | Number           | Fast forward by the specified seek time. If no parameter is passed, the default seek time will be used.    |
| `increaseVolume(step)`   | Number           | Increase volume by the specified step. If no parameter is passed, the default step will be used.           |
| `decreaseVolume(step)`   | Number           | Increase volume by the specified step. If no parameter is passed, the default step will be used.           |
| `toggleCaptions(toggle)` | Boolean          | Toggle captions display. If no parameter is passed, it will toggle based on current status.                |
| `fullscreen.enter()`     | -                | 进入全屏. 如果该设备不支持全屏, 取而代之的是回退“全窗口/视窗”。.                                                 |
| `fullscreen.exit()`      | -                | 退出全屏.                                                                                           |
| `fullscreen.toggle()`    | -                | 切换全屏状态.                                                                                         |
| `airplay()`              | -                | 在支持airplay的设备里（一般是苹果设备），弹出airplay弹出框                                                         |
| `toggleControls(toggle)` | Boolean          | Toggle the controls (video only). Takes optional truthy value to force it on/off.                          |
| `on(event, function)`    | String, Function | 为指定事件添加事件侦听.                                                                                 |
| `once(event, function)`  | String, Function | 为指定事件添加一次性的事件侦听。                                                        |
| `off(event, function)`   | String, Function | 移除指定事件的事件侦听                                                                                      |
| `supports(type)`         | String           | 检查对多媒体文件格式的支持性。                                                                               |
| `destroy()`              | -                | 销毁Plyr实例，启动垃圾回收机制                                                                                  |

1.  对于HTML5播放器, 在 _一些_ 浏览器里`play()` 会返回一个 [`Promise`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) 对象 - WebKit 和 Mozilla [根据MDN](https://developer.mozilla.org/en-US/docs/Web/API/HTMLMediaElement/play) at time of writing.

## Getters 和 Setters

setters范例:

```javascript
player.volume = 0.5; // Sets volume at 50%
player.currentTime = 10; // Seeks to 10 seconds
```

getters范例:

```javascript
player.volume; // 0.5;
player.currentTime; // 10
player.fullscreen.active; // false;
```

| 属性             | Getter | Setter | 说明                                                                                                                                                                                                                                                                                                                                   |
| -------------------- | ------ | ------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `isHTML5`            | ✓      | -      | 返回一个布尔值，表示当前播放器是否为HTML5。                                                                                                                                                                                                                                                                         |
| `isEmbed`            | ✓      | -      | 返回一个布尔值，表示当前播放器是否为嵌入式播放器。                                                                                                                                                                                                                                                      |
| `playing`            | ✓      | -      | 返回一个布尔值，表示当前播放器是否在播放.                                                                                                                                                                                                                                                                         |
| `paused`             | ✓      | -      | 返回一个布尔值，表示当前播放器是否在暂停中.                                                                                                                                                                                                                                                                          |
| `stopped`            | ✓      | -      | 返回一个布尔值，表示当前播放器是否已经停止.                                                                                                                                                                                                                                                                         |
| `ended`              | ✓      | -      | 返回一个布尔值，表示当前播放器是否播放完成。                                                                                                                                                                                                                                                             |
| `buffered`           | ✓      | -      | 返回一个介于0和1之间的浮点数，表示当前媒体缓冲了多少                                                                                                                                                                                                                                                      |
| `currentTime`        | ✓      | ✓      | 获取或设置播放器的当前时间。setter接受以秒为单位的浮点数（float）。                                                                                                                                                                                                                                                   |
| `seeking`            | ✓      | -      | Returns a boolean indicating if the current player is seeking.                                                                                                                                                                                                                                                                         |
| `duration`           | ✓      | -      | 返回当前媒体的持续时间。                                                                                                                                                                                                                                                                                           |
| `volume`             | ✓      | ✓      | 获取或设置播放器的音量。setter接受一个介于0和1之间的浮点数（float）。                                                                                                                                                                                                                                                   |
| `muted`              | ✓      | ✓      | 获取或设置播放器的静音状态. setter接受一个布尔值.                                                                                                                                                                                                                                                              |
| `hasAudio`           | ✓      | -      | 返回一个布尔值，表示当前媒体是否有音频曲目。                                                                                                                                                                                                                                                                  |
| `speed`              | ✓      | ✓      | Gets or sets the speed for the player. The setter accepts a value in the options specified in your config. Generally the minimum should be 0.5.                                                                                                                                                                                        |
| `quality`&sup1;      | ✓      | ✓      | Gets or sets the quality for the player. The setter accepts a value from the options specified in your config.                                                                                                                                                                                                                         |
| `loop`               | ✓      | ✓      | Gets or sets the current loop state of the player. The setter accepts a boolean.                                                                                                                                                                                                                                                       |
| `source`             | ✓      | ✓      | Gets or sets the current source for the player. The setter accepts an object. See [source setter](#the-source-setter) below for examples.                                                                                                                                                                                              |
| `poster`             | ✓      | ✓      | Gets or sets the current poster image for the player. The setter accepts a string; the URL for the updated poster image.                                                                                                                                                                                                               |
| `autoplay`           | ✓      | ✓      | Gets or sets the autoplay state of the player. The setter accepts a boolean.                                                                                                                                                                                                                                                           |
| `currentTrack`       | ✓      | ✓      | Gets or sets the caption track by index. `-1` means the track is missing or captions is not active                                                                                                                                                                                                                                     |
| `language`           | ✓      | ✓      | Gets or sets the preferred captions language for the player. The setter accepts an ISO two-letter language code. Support for the languages is dependent on the captions you include. If your captions don't have any language data, or if you have multiple tracks with the same language, you may want to use `currentTrack` instead. |
| `fullscreen.active`  | ✓      | -      | 返回一个布尔值，表示当前播放器是否在全屏模式中                                                                                                                                                                                                                                                              |
| `fullscreen.enabled` | ✓      | -      | 返回一个布尔值，表示当前播放器是否已启用全屏                                                                                                                                                                                                                                                            |
| `pip`&sup1;          | ✓      | ✓      | Gets or sets the picture-in-picture state of the player. The setter accepts a boolean. This currently only supported on Safari 10+ (on MacOS Sierra+ and iOS 10+) and Chrome 70+.                                                                                                                                                      |
| `ratio`              | ✓      | ✓      | Gets or sets the video aspect ratio. The setter accepts a string in the same format as the `ratio` option.                                                                                                                                                                                                                             |
| `download`           | ✓      | ✓      | 获取或设置下载按钮的URL。setter接受包含有效URL的字符串。                                                                                                                                                                                                                            |

1.  仅HTML5

### `.source` setter

允许在运行中更改播放器源和类型。

Video范例:

```javascript
player.source = {
    type: 'video',
    title: 'Example title',
    sources: [
        {
            src: '/path/to/movie.mp4',
            type: 'video/mp4',
            size: 720,
        },
        {
            src: '/path/to/movie.webm',
            type: 'video/webm',
            size: 1080,
        },
    ],
    poster: '/path/to/poster.jpg',
    tracks: [
        {
            kind: 'captions',
            label: 'English',
            srclang: 'en',
            src: '/path/to/captions.en.vtt',
            default: true,
        },
        {
            kind: 'captions',
            label: 'French',
            srclang: 'fr',
            src: '/path/to/captions.fr.vtt',
        },
    ],
};
```

Audio范例:

```javascript
player.source = {
    type: 'audio',
    title: 'Example title',
    sources: [
        {
            src: '/path/to/audio.mp3',
            type: 'audio/mp3',
        },
        {
            src: '/path/to/audio.ogg',
            type: 'audio/ogg',
        },
    ],
};
```

YouTube范例:

```javascript
player.source = {
    type: 'video',
    sources: [
        {
            src: 'bTqVqk7FSmY',
            provider: 'youtube',
        },
    ],
};
```

_注意_: `src` 可以是video ID或者URL

Vimeo范例

```javascript
player.source = {
    type: 'video',
    sources: [
        {
            src: '143418951',
            provider: 'vimeo',
        },
    ],
};
```

_注意:_ YouTube和Vimeo的`src`属性可以是video ID或者URL

| 属性       | 类型   | 说明                                                                                                                                                                                                                                                                                                                                                                                                    |
| -------------- | ------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `type`         | String | Either `video` or `audio`. _Note:_ YouTube and Vimeo are currently not supported as audio sources.                                                                                                                                                                                                                                                                                                             |
| `title`        | String | _Optional._ Title of the new media. Used for the `aria-label` attribute on the play button, and outer container. YouTube and Vimeo are populated automatically.                                                                                                                                                                                                                                                |
| `sources`      | Array  | This is an array of sources. For HTML5 media, the properties of this object are mapped directly to HTML attributes so more can be added to the object if required.                                                                                                                                                                                                                                             |
| `poster`&sup1; | String | The URL for the poster image (HTML5 video only).                                                                                                                                                                                                                                                                                                                                                               |
| `tracks`&sup1; | String | An array of track objects. Each element in the array is mapped directly to a track element and any keys mapped directly to HTML attributes so as in the example above, it will render as `<track kind="captions" label="English" srclang="en" src="https://cdn.selz.com/plyr/1.0/example_captions_en.vtt" default>` and similar for the French version. Booleans are converted to HTML5 value-less attributes. |

1.  仅HTML5

# 事件

您可以监听并设置Plyr的目标元素上的事件（参见表下的示例）。有些事件只适用于HTML5音频和视频。 当使用对实例的引用时，你可以可以使用`on()`API方法或`addEventListener()`。 你可以通过这个`event.detail.plyr`可以获得对api的访问.。下面有个例子:

```javascript
player.on('ready', event => {
    const instance = event.detail.plyr;
});
```

## 标准媒体事件

| 事件种类            | 说明                                                                                                                                                                                                            |
| ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `progress`         | Sent periodically to inform interested parties of progress downloading the media. Information about the current amount of the media that has been downloaded is available in the media element's `buffered` attribute. |
| `playing`          | Sent when the media begins to play (either for the first time, after having been paused, or after ending and then restarting).                                                                                         |
| `play`             | Sent when playback of the media starts after having been paused; that is, when playback is resumed after a prior `pause` event.                                                                                        |
| `pause`            | 当播放暂停的时候触发                                                                                                                                                                                      |
| `timeupdate`       | The time indicated by the element's `currentTime` attribute has changed.                                                                                                                                               |
| `volumechange`     | 当音频音量发生改变的时候触发 (设置音量大小和改变静音`muted`状态也会触发)。                                                                                                              |
| `seeking`          | Sent when a seek operation begins.                                                                                                                                                                                     |
| `seeked`           | Sent when a seek operation completes.                                                                                                                                                                                  |
| `ratechange`       | 当播放速度改变的时候触发                                                                                                                                                                                 |
| `ended`            | 当播放完成的时候触发 . _N注意:_ 如果`autoplay`true，那么这个事件就不会触发                                                                                                                                  |
| `enterfullscreen`  | 当播放器进入全屏状态的时候触发(对于较旧的浏览器，可以选择适当的全屏或全窗口回退).                                                                                                 |
| `exitfullscreen`   | 当播放器退出全屏状态的时候触发                                                                                                                                                                            |
| `captionsenabled`  | 当字幕生效的时候触发                                                                                                                                                                                      |
| `captionsdisabled` | 当字幕失效的时候触发                                                                                                                                                                                      |
| `languagechange`   | 当字幕语言发生改变的时候触发                                                                                                                                                                             |
| `controlshidden`   | 当控制条隐藏的时候触发                                                                                                                                                                                    |
| `controlsshown`    | 当控制条显示的时候触发                                                                                                                                                                                     |
| `ready`            |当实例准备好进行api调用时触发。                                                                                                                                                                    |

### 仅HTML5

| 事件种类       | 说明                                                                                                                                                                                                                                                                                                                                    |
| ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `loadstart`      | 当媒体开始加载的时候触发                                                                                                                                                                                                                                                                                                         |
| `loadeddata`     | 当媒体的第1帧已经加载完成的时候触发                                                                                                                                                                                                                                                                                            |
| `loadedmetadata` | 当媒体的元数据加载完成的时候触发 ；所有属性现在包含的有用信息与它们将要包含的一样多。                                                                                                                                                                                                             |
| `qualitychange`  | 当视频质量发生改变的时候触发                                                                                                                                                                                                                            |
| `canplay`        | 当有足够的数据可以播放媒体时（至少可以播放几帧）触发。这相当于 `HAVE_ENOUGH_DATA` `readyState`                                                                                                                                                                                    |
| `canplaythrough` | Sent when the ready state changes to `CAN_PLAY_THROUGH`, indicating that the entire media can be played without interruption, assuming the download rate remains at least at the current level. _Note:_ Manually setting the `currentTime` will eventually fire a `canplaythrough` event in firefox. Other browsers might not fire this event. |

| `stalled`        | 当用户代理（UA）尝试获取媒体数据,数据却据意外地无法提供的时候触发。                                                                                                                                                                                         |
| `waiting`        | 当请求的操作（如回放）延迟等待另一个操作（如条状）完成时发送                                                                                                                                                                                                                 |
| `emptied`        | he media has become empty; for example, this event is sent if the media has already been loaded (or partially loaded), and the `load()` method is called to reload it.                                                                                                                                                                         |
| `cuechange`      | 当`TextTrack`更改了当前显示的提示时触发。                                                                                                                                                                                                                                                                      |
| `error`          | 当有错误发生的时候触发. 元素的`error`属性包含更多信息。                                                                                                                                                                                                                                                   |

### 仅YouTube

| 事件种类    | 说明                                                                                                                                                                                                                                                                                                                |
| ------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `statechange` | 播放器状态发生改变，可以通过`event.detail.code`访问该参数，可能的值是 `-1`: 未开始, `0`: 结束了, `1`: 播放中, `2`: 暂停, `3`: 缓冲中。你可以查看 [YouTube文档](https://developers.google.com/youtube/iframe_api_reference#onStateChange)获取更多信息。 |

_注意:_ 这些在DOM里面是冒泡事件。而事件对象则是容器元素。

一些事件的细节是引入自[MDN](https://developer.mozilla.org/en-US/docs/Web/Guide/Events/Media_events)的。


# 嵌入式

目前支持YouTube和Vimeo，其功能非常类似于HTML5视频，类似的事件和api方法可用于所有类型。但是如果您希望直接访问api，你可以通过Plyr播放器对象的`embed`属性执行此操作，例如`player.embed`，然后可以使用第三方API了。有关各自API的更多信息，请参见：

-   [YouTube iframe API指南](https://developers.google.com/youtube/iframe_api_reference)
-   [Vimeo player.js指南](https://github.com/vimeo/player.js)

_Note_: 并非所有的API方法都能100%正常工作，因为你的环境可能不同，最好尽可能使用Plyr API。
# 键盘快捷键

默认情况下，当播放器被聚焦（foucs）的时候，它将绑定以下键盘快捷键。如果你的`global`配置设置为`true` 并且只有一个播放器时，那么除需要输入的元素外，任何元素都被聚焦（foucs）时，快捷键都将起作用。


| 键位        | 操作                                 |
| ---------- | -------------------------------------- |
| `0` to `9` | 分别从从0到90%的进度跳转视频      |
| `space`    | 切换播放暂停状态                       |
| `K`        | 切换播放暂停状态                         |
| &larr;     | 后退视频 （受`seekTime` 选项影响）               |
| &rarr;     | 前进视频 （受`seekTime` 选项影响）               |
| &uarr;     | 增大音量                                |
| &darr;     | 减少音量                                |
| `M`        | 切换静音状态                            |
| `F`        | 切换全屏状态                            |
| `C`        | 切换字幕开关状态                        |
| `L`        | 切换循环播放状态                            |

# 预览缩略图

当您将鼠标悬停在进度条上或在视频区域时，可以根据演示显示预览缩略图，可以用于所有视频种类（HTML、Youtube、Vimeo等）。而HTML5来说是最简单的，你需要自己生成雪碧图或图像，使用aws转码器来生成帧，然后将它们组合成雪碧图。出于性能方面的考虑，建议使用雪碧图，因为它们下载速度更快，压缩成小文件大小也更容易，因此加载速度更快。

您可以在[这里](https://cdn.plyr.io/static/demo/thumbs/100p.vtt)和[这里](https://cdn.plyr.io/static/demo/thumbs/240p.vtt)看到示例vtt文件，了解雪碧图是如何完成的。坐标按x偏移量（X Offset）、y偏移量（Offset）、宽度（Width）、高度（Height）的顺序设置为url上的`xywh` Hash(例如，`240p-00001.jpg#xywh=1708,480,427,240`代表左偏移量为`1708px`，上偏移量为 `480px`，宽高为`427x240px`）。如果你想把每帧图像都包含进去，这是也是可以的，但会比较慢，带来不好的体验。

# 全屏

Plyr的全屏功能支持大多数现代浏览器，你可以从[这里](http://caniuse.com/#feat=fullscreen)查看全屏功能的浏览器适配程度。

# 浏览器兼容性

Plyr支持大多数 _现代_ 浏览器的最新的两个版本。


| Browser       | Supported     |
| ------------- | ------------- |
| Safari        | ✓             |
| Mobile Safari | ✓&sup1;       |
| Firefox       | ✓             |
| Chrome        | ✓             |
| Opera         | ✓             |
| Edge          | ✓             |
| IE11          | ✓&sup3;       |
| IE10          | ✓&sup2;&sup3; |

1.  除非你设置“playsinline”属性，否则在iPhone上的safari浏览器会强制使用ios自带播放器渲染`<video>`，同时音量控制也被禁用，因为视频的音量控制只能由ios设备控制。
2.  Native player used (不支持 `<progress>` 或者 `<input type="range">`) but the API is supported. No native fullscreen support, fallback can be used (你可以查看文档的 [options](#options)部分).
3.  需要使用Polyfills. 见下文.

## Polyfills

由于Plyr使用ES6，所以并不能完全支持的所有浏览器。这意味着某些功能需要使用Polyfills才能使用，否则会遇到问题。我们选择不让90%的用户使用额外的js来支持这些特性，而是让polyfill根据您的需要来解决问题。我找到的最简单的方法是使用[polyfill.io]（https://polyfill.io），它提供基于用户代理的Polyfills。这是也是Demo里使用的方法。


## 检查当前环境是否支持Plyr

您可以使用静态方法检查当前环境是否支持Plyr。例如

```javascript
const supported = Plyr.supported('video', 'html5', true);
```

参数分别是:

-   类型 (`audio` 或 `video`)
-   提供程序 (`html5`, `youtube` 或 `vimeo`)
-   播放器是否具有 `playsinline` 属性 (仅适用于iOS 10+)

## 禁用Plyr支持

`enabled`选项可用于禁用某些UA(指的是设备类型)的Plyr功能。例如，如果您不想将Plyr用于智能手机，如下所示：


```javascript
{
    enabled: /Android|webOS|iPhone|iPad|iPod|BlackBerry/i.test(navigator.userAgent);
}
```

如果你的设备被禁用了Plyr，但是支持原生的 `<video>` 和 `<audio>`标签, 则会使用设备的原生播放器.

# 插件 & 组件

有一群给力的老哥为Plyr开发了CMS插件和一些JavaScript框架的组件：

| Type      | 维护者                                                     | 链接                                                                                         |
| --------- | -------------------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| WordPress | Brandon Lavigne ([@drrobotnik](https://github.com/drrobotnik)) | [https://wordpress.org/plugins/plyr/](https://wordpress.org/plugins/plyr/)                   |
| Angular   | Simon Bobrov ([@smnbbrv](https://github.com/smnbbrv))          | [https://github.com/smnbbrv/ngx-plyr](https://github.com/smnbbrv/ngx-plyr)                   |
| React     | Jose Miguel Bejarano ([@xDae](https://github.com/xDae))        | [https://github.com/xDae/react-plyr](https://github.com/xDae/react-plyr)                     |
| Vue       | Gabe Dunn ([@redxtech](https://github.com/redxtech))           | [https://github.com/redxtech/vue-plyr](https://github.com/redxtech/vue-plyr)                 |
| Neos      | Jon Uhlmann ([@jonnitto](https://github.com/jonnitto))         | [https://packagist.org/packages/jonnitto/plyr](https://packagist.org/packages/jonnitto/plyr) |
| Kirby     | Dominik Pschenitschni ([@dpschen](https://github.com/dpschen)) | [https://github.com/dpschen/kirby-plyrtag](https://github.com/dpschen/kirby-plyrtag)         |

# Issues

如果你在Plyr中遇到一些诡异的现象或者Bug，请在GitHub Issues提出来。


# 作者

Plyr主要是由[@sam_potts](https://twitter.com/sam_potts) / [sampotts.me](http://sampotts.me)开发的，当然也少不了一众[contributors](https://github.com/sampotts/plyr/graphs/contributors)的帮助


# 捐献

一直以来我很享受开发Plyr的过程，因此我一直都是无偿开发Plyr项目，开源并免费给大家使用。但由于开发并运营Plyr项目不仅仅花我了很多时间，我还需要为域名、服务器托管等支付不少费用。如果你觉得Plyr不错或者帮到了你，你可以给Plyr捐献以维持项目开销，谢谢…

-   [通过Patreon捐献](https://www.patreon.com/plyr)
-   [通过PayPal捐献](https://www.paypal.me/pottsy/20usd)

# 被提及

-   [ProductHunt](https://www.producthunt.com/tech/plyr)
-   [The Changelog](http://thechangelog.com/plyr-simple-html5-media-player-custom-controls-webvtt-captions/)
-   [HTML5 Weekly #177](http://html5weekly.com/issues/177)
-   [Responsive Design #149](http://us4.campaign-archive2.com/?u=559bc631fe5294fc66f5f7f89&id=451a61490f)
-   [Web Design Weekly #174](https://web-design-weekly.com/2015/02/24/web-design-weekly-174/)
-   [Front End Focus #177](https://frontendfoc.us/issues/177)
-   [Hacker News](https://news.ycombinator.com/item?id=9136774)
-   [Web Platform Daily](http://webplatformdaily.org/releases/2015-03-04)
-   [LayerVault Designer News](https://news.layervault.com/stories/45394-plyr--a-simple-html5-media-player)
-   [The Treehouse Show #131](https://teamtreehouse.com/library/episode-131-origami-react-responsive-hero-images)
-   [noupe.com](http://www.noupe.com/design/html5-plyr-is-a-responsive-and-accessible-video-player-94389.html)

# 使用了Plyr的公司或项目

-   [Selz.com](https://selz.com)
-   [Peugeot.fr](http://www.peugeot.fr/marque-et-technologie/technologies/peugeot-i-cockpit.html)
-   [Peugeot.de](http://www.peugeot.de/modelle/modellberater/208-3-turer/fotos-videos.html)
-   [TomTom.com](http://prioritydriving.tomtom.com/)
-   [DIGBMX](http://digbmx.com/)
-   [Grime Archive](https://grimearchive.com/)
-   [koel - A personal music streaming server that works.](http://koel.phanan.net/)
-   [Oscar Radio](http://oscar-radio.xyz/)
-   [Sparkk TV](https://www.sparkktv.com/)
-   [@halfhalftravel](https://www.halfhalftravel.com/)

如果你的项目使用了Plyr并想把项目添加到上面的列表中, 你可以开个PR。 我们会很开心的看到你是如何使用Plyr的  😎

# 实用链接

Plyr的字幕功能最初是从PayPal的HTML5视频播放器移植过来的:

-   [PayPal开发的HTML5视频播放器](https://github.com/paypal/accessible-html5-video-player)
-   一个由[@arayutw](https://twitter.com/arayutw)写的[日文版Plyr指南!](http://syncer.jp/how-to-use-plyr-io)

# 致谢

[![Fastly](https://cdn.plyr.io/static/fastly-logo.png)](https://www.fastly.com/)

感谢 [Fastly](https://www.fastly.com/) 提供了CDN托管服务

[![Sentry](https://cdn.plyr.io/static/sentry-logo-black.svg)](https://sentry.io/)

感谢[Sentry](https://sentry.io/)为demo站点提供日志服务。


# 版权和许可

[The MIT license](license.md)
