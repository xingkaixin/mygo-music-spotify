# Spotify for MyGo Music

[English](README.md) | 简体中文

在 [MyGo Music](https://github.com/egoist/mygo-music) 里浏览和控制 Spotify。本插件与 Spotify 无关，也未经其认可。

声音来自一台 Spotify Connect 设备：本机或手机上的 Spotify 官方 App、音箱，或你的账号能播放的其他设备。MyGo Music 负责展示你的曲库，并告诉那台设备播什么。装了 [librespot](https://github.com/librespot-org/librespot) 之后，本机不开 Spotify App 也能当作这样一台设备。

**播放需要 Spotify Premium。**

## 设置

1. 用 Premium 账号登录 [Spotify 开发者后台](https://developer.spotify.com/dashboard)，点 **Create app**。名称和描述随便填，添加下面这个 Redirect URI，勾选 **Web API**，同意条款后保存：

   ```
   http://127.0.0.1:43110/callback
   ```

   必须一字不差：写成 `localhost` 或末尾多一个斜杠都不行。
2. 用 deeplink 安装插件：

   [mygo-music://install-plugin?repo=xingkaixin/mygo-music-spotify](mygo-music://install-plugin?repo=xingkaixin/mygo-music-spotify)

   或者在 设置 > 插件 里粘贴 GitHub 地址：

   [https://github.com/xingkaixin/mygo-music-spotify](https://github.com/xingkaixin/mygo-music-spotify)
3. 在开发者后台的 App 页面复制 **Client ID**，粘贴到 MyGo Music 里这个插件的设置中，点 **登录**，然后在浏览器里批准授权。
4. 在某台设备上打开 Spotify，或者按下文配置 librespot，然后在 MyGo Music 里播放。想换设备，在播放器的设备菜单里选。

只有创建这个 App 的账号，以及被加进 App 的账号能登录。Spotify 的 Development Mode 最多允许 5 个账号。要加人，在后台打开这个 App，进入 **User Management**，填入对方账号的名字和邮箱。

## 不开 Spotify App 播放

1. 用 Homebrew 安装 librespot。插件只在 Homebrew 的目录里找它：`/opt/homebrew/bin` 和 `/usr/local/bin`。

   ```
   brew install librespot
   ```
2. 在 MyGo Music 里打开 设置 > 插件 > Spotify，点 **允许启动程序**。
3. 播放一首歌。第一次会在浏览器里打开一个 Spotify 页面，给 librespot 登录。这是独立于插件登录的另一次登录，用同一个账号批准。如果那首歌还没开始播，再点一次播放。

librespot 在本机以 320 kbps 播放，设备名是 **MyGo Music**。没有其他设备在播、你也没在设备菜单里选过别的设备时，就用它。它在你第一次播放时启动，MyGo Music 退出时结束。

要让 librespot 换一个账号：退出 MyGo Music，删除 `~/Library/Application Support/MyGo Music/plugin-data/spotify/librespot`，再播放一次。

对部分账号，尤其是较新的账号，Spotify 会拒绝给 librespot 歌曲密钥，结果是什么都播不出来（[librespot#1649](https://github.com/librespot-org/librespot/issues/1649)）。遇到这种情况，改用 Spotify App 播放。

## MyGo Music Queue 歌单

Spotify 桌面 App 不播放直接发给它的歌曲列表，只播放歌单或专辑。所以第一次播放时，插件会在你的曲库里建一个名为 **MyGo Music Queue** 的私密歌单。每次播放，插件把接下来要播的歌（最多 100 首）写进这个歌单，再播放它。MyGo Music 的侧边栏会隐藏它，Spotify 的 App 里能看到。不要编辑它：每次播放都会重写。如果删了，下次播放时插件会再建一个。

## 支持的功能

- 首页：最近播放、常听歌曲、常听艺人、收藏的专辑
- 搜索歌曲、专辑、艺人、歌单和播客
- 专辑、艺人、你的歌单、喜欢的歌曲、收藏的专辑和播客
- 喜欢歌曲，收藏专辑、歌单和播客
- 新建、重命名、删除歌单，添加、移除、调整歌单里的歌曲顺序
- 播放、暂停、拖动进度、音量、选择设备
- 来自 [LRCLIB](https://lrclib.net) 的滚动歌词（有收录时）

## Spotify 不允许的功能

Spotify 给 Development Mode 应用开放的 Web API 比它自家 App 少：

- 不是你创建、也不是你参与协作的歌单（包括 Spotify 官方歌单）会出现在侧边栏，但打不开。
- 没有编辑推荐、排行榜、新歌速递、推荐和电台。
- 拿不到艺人的热门歌曲。艺人页显示的是搜索这个艺人名字时排在前面的歌。
- 不能关注艺人。
- 搜索每页只返回 10 条结果。

## 常见问题

下面加粗的是 Spotify 页面或 MyGo Music 里显示的原文。

**Invalid redirect URI**（登录时 Spotify 页面显示）：后台里的 App 没有一字不差地填 `http://127.0.0.1:43110/callback`。补上、保存，再登录一次。

**Spotify won't let this account in: add it under User Management in your app's dashboard, and check the app's owner has Premium**（登录后显示）：Spotify 的 Development Mode 只允许创建 App 的账号和加进 **User Management** 的账号使用，而且创建 App 的账号要有有效的 Premium。如果浏览器里登录的是另一个 Spotify 账号，先在浏览器里退出它。处理好对应的问题后，再登录一次。

**Open Spotify on this computer, your phone or a speaker, then play again**：没有在线的 Spotify 设备。在某台设备上打开 Spotify App，或者配置 librespot。librespot 第一次登录完成后，再点一次播放。

**Playing through Spotify needs Premium**：登录的账号是 Spotify Free。

**Spotify is limiting requests: try again in a moment**：Spotify 限制 Development Mode 应用的请求频率和总量。额度按你的开发者账号计算，所以多建一个 App 没用。等一会儿再试。

**需要代理才能访问 Spotify 时，什么都加载不出来**：MyGo Music 和 librespot 直接连接 Spotify，不走系统代理设置。打开代理软件的 TUN 模式（有的叫增强模式）。

## 隐私

你的 Spotify token 以明文保存在本机的插件数据里，只发给 Spotify。退出登录会删除它们；librespot 的登录信息保存在插件数据的 `librespot` 文件夹里，删除前一直有效。要在 Spotify 那边撤销授权，到 Spotify 账号的 **Manage apps** 页面移除这个 App。

每首歌的标题、艺人、专辑和时长会发给 LRCLIB 来查歌词。
