# bili_UP_data_card

bilibili UP主信息卡片生成，支持使用Actions自动更新

[![generate_up_card](https://github.com/Little-Data/bili_UP_data_card/actions/workflows/generate_up_card.yml/badge.svg)](https://github.com/Little-Data/bili_UP_data_card/actions/workflows/generate_up_card.yml) [![get_UP_data_json](https://github.com/Little-Data/bili_UP_data_card/actions/workflows/get_UP_data_json.yml/badge.svg)](https://github.com/Little-Data/bili_UP_data_card/actions/workflows/get_UP_data_json.yml)

# 成果预览

<div align="center">

<img height="450px" src="/bili/UP_card_light.png#gh-light-mode-only" />
<img height="450px" src="/bili/UP_card_dark.png#gh-dark-mode-only" />

</div>

<div align="center">
图片可根据主题自动切换浅色/深色
</div>

# 特点

支持命令行参数，指定输出输入目录，有浅色/深色模式两张图片

### 浅色模式图片

<div align="center">

<img height="450px" src="/bili/UP_card_light.png" />

</div>

### 深色模式图片

<div align="center">

<img height="450px" src="/bili/UP_card_dark.png" />

</div>

# 深入探索

**GitHub Actions**

使用之前请到仓库设置中`Actions` `General` `Workflow permissions`下，选`Read and write permissions`

如果你fork来使用的话，确保同页面的`Actions permissions`部分选了`Allow all actions and reusable workflows`

<img width="2872" height="1832" alt="PixPin_2025-12-08_13-00-09" src="https://github.com/user-attachments/assets/70ec78c6-a366-4a2c-9e81-f9454c8b0097" />

也可以自行创建`.github/workflows`文件夹，将文件复制过去。

完成后请自行手动运行一次。

**程序说明**

`get_UP_data.py` 使用api获取信息程序，获取到的信息保存为json文件

命令行：

```py
-m  --mid B站用户ID
-o  --output 输出文件路径
```

`UP_data_gen_img.py`将获取到的json文件提取信息，放入HTML模板，输出图片

命令行：

```py
--input 输入JSON数据文件路径
--output 输出图片基础路径（不含后缀）
```
注意，`UP_data_gen_img.py`输出图片基础路径如果写成`./bili`那么会在`程序所在目录`下生成两张`bili`前缀的图片，而不是在`bili`目录下生成。

**使用生成的图片**

在GitHub上使用自动切换浅色/深色的图片很简单
```
![](/图片路径/图片名_light.png#gh-light-mode-only)  浅色

![](/图片路径/图片名_dark.png#gh-dark-mode-only) 深色

使用img标签（可设置图片的宽和高，这里只设置高）

<img height="450px" src="/图片路径/图片名_light.png#gh-light-mode-only" />  浅色
<img height="450px" src="/图片路径/图片名_dark.png#gh-dark-mode-only" /> 深色
```

两句同时写即可，GitHub会根据主题自动切换，也可以这样写：

```html
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="/图片路径/图片名_light.png" />  浅色
  <source media="(prefers-color-scheme: light)" srcset="/图片路径/图片名_dark.png" /> 深色
  <img alt="github-snake" src="/图片路径/图片名.png" />  无法检测颜色模式时的默认图片
</picture> 
```

一些没有提到的可以自行探索本仓库的写法。

**在本地电脑上运行**

python 要求：3.13+（开发时的环境）

依赖：

```
aiohttp
playwright

playwright install chromium
```
Windows 额外依赖

```
tzdata
```

HTML模板中引用了字体文件，如果缺少可自行安装。一般情况下Windows是不缺的，Linux上是缺少的，如果不装生成的图片中文会变为方块豆腐。HTML模板字体也可以自行修改（不是修改这里的安装依赖清单）。

```
fonts-roboto
fonts-oxygen
fonts-cantarell
fonts-noto
```

# 灵感

[bilibili-API-collectapi](https://github.com/SocialSisterYi/bilibili-API-collect)接口文档，一切的基础。

# license

CC BY-NC-SA 4.0

[署名—非商业性使用—相同方式共享 4.0 协议国际版](https://creativecommons.org/licenses/by-nc-sa/4.0/legalcode.zh-hans)

![Star History Chart](https://api.star-history.com/svg?repos=Little-Data/bili_UP_data_card&type=date&legend=top-left)
