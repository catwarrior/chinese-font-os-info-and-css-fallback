# 中文排版常用字体 的 操作系统安装情况 和 CSS Fallback 方案 ![](https://img.shields.io/badge/release-no-red.svg?style=flat-square)


## 操作系统默认字体

**PC**

操作系统   | 宋体           | 黑体          | 楷体         | 仿宋体
--------- | ------------- | ------------ | ------------ | -------------
Win XP    | 宋体（SimSun）, 新宋体（NSimSun）, 新细明體（PMingLiu）| 黑体（SimHei） | 楷体（Kaiti_GB2312）, 微軟標楷（DFKai-SB） | 仿宋（Fangsong_GB2312）
Win 7     | 宋体（SimSun）, 新宋体（NSimSun）, 细明體（MingLiU）, 新细明體（PMingLiu） | 黑体（SimHei）, 微软雅黑（Microsoft YaHei）, 微軟正黑體（Microsoft JhengHei） | 楷体（Kaiti）, 微軟標楷（DFKai-SB）| 仿宋（Fangsong）
Win 8     | 宋体（SimSun）, 新宋体（NSimSun）, 细明體（MingLiU）, 新细明體（PMingLiu）, 华文宋体（STSong）| 黑体（SimHei）, 微软雅黑（Microsoft YaHei）, 微軟正黑體（Microsoft JhengHei）, 华文细黑（STXihei） | 楷体（Kaiti）, 微軟標楷（DFKai-SB）, 华文楷体（STKaiti）| 仿宋（Fangsong）, 华文仿宋（STFangsong）
OS X      | 华文宋体（STSong）,儷宋 Pro（LiSong Pro）| 冬青黑体简体中文 （Hiragino Sans GB）, 华文黑体（STHeiti）, 兰亭黑（LantingHei）, 儷黑 Pro（LiHei Pro） | 华文楷体（STKaiti） | 华文仿宋（STFangsong）

> - 根据 [百度统计 - 操作系统份额报告](http://tongji.baidu.com/data/os) 排序, 截止 2015-5
> - Windows 字体信息 [Microsoft Typography - Fonts and Products](http://www.microsoft.com/typography/fonts/product.aspx#Windows)  
> - OS X 字体信息 [Mac OS X v10.6: Fonts list](https://support.apple.com/en-us/HT202408)

**Mobile**

操作系统 | 宋体   | 黑体                       | 楷体         | 仿宋体
-------- | ----- | ------------------------- | ------------ | -------------
Android  | -     | Roboto, DroidSansFallback | -            | -
iOS      | -     | Heiti SC                  | -            | -

>  - Android 字体信息 [Android Design - Typography](http://developer.android.com/design/style/typography.html)
>  - iOS 字体信息 [iOS Fonts](http://iosfonts.com/) 

**待修订**

- Win 2003 占有率统计也列入前五，暂未考虑
- Linux, Ubuntu 系统未覆盖
- 明朝體（MS Mincho）定义为日文字体，要归类到宋体么？

## CSS Fallback

- 宋体

```
font-family: 'Arial Narrow', 'Times New Roman', STSong, '宋体', serif;
```

- 黑体

```
font-family: Helvetica, Arial, 'Hiragino Sans GB', 'Microsoft Yahei', '黑体', sans-serif;
```

- 楷体

```
font-family: 'Times New Roman', STKaiti, KaiTi, '楷体', serif;
```

- 仿宋体

```
font-family: 'Times New Roman', STFangSong, FangSong, '仿宋', serif;
```

**使用 [`lang`](http://www.w3.org/TR/html5/dom.html#the-lang-and-xml:lang-attributes) 区分 繁体、简体，楷体为例**  

```
:lang(zh-Hans) {
    font-family: 'Times New Roman', STKaiti, KaiTi, '楷体', serif;
}

:lang(zh-Hant) {
    font-family: 'Times New Roman', DFKai-SB, STKaiti, KaiTi, '楷体', serif;
}
```

关于 `Fallback` 还有一个更巧妙的解决方案，来自 [`Han.css`](https://github.com/ethantw/Han)：

- 黑体 GB (中國國標)

```
@font-face {
  font-family: 'Han Heiti GB';
  src:
    local('Hiragino Sans GB'),
    local('Lantinghei SC'),
    local('Heiti SC'),

    local('Microsoft Yahei'),

    local('Droid Sans Fallback')
  ;
   unicode-range: U+"+270C";
}
```
 
[`unicode-range`](http://dev.w3.org/csswg/css-fonts/#descdef-unicode-range) 在 IE8-, Firefox 上有兼容性问题，加上不可避免的中英文混排场景，还是推荐使用 `font-famliy` 解决 `Fallback` 问题

> [can i use - unicode-range](http://caniuse.com/#search=unicode-range)
