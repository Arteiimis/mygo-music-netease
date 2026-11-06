# 网易云音乐 · MyGo Music 插件

在 [MyGo Music](https://github.com/egoist/mygo-music) 里播放网易云音乐：登录、发现音乐、每日推荐、我的歌单、搜索、歌手与专辑、播客、私人 FM、心动模式、评论与逐字歌词。

与网易云音乐官方无关，使用的是网易云的私有接口，随时可能失效。音乐版权归各权利人所有。

## 安装

需要 **MyGo Music 0.1.8 或更高版本**。

[安装网易云音乐插件](mygo-music://install-plugin?repo=Arteiimis/mygo-music-netease)

或在 **设置 > 插件 > +** 里粘贴 `Arteiimis/mygo-music-netease`。不需要额外的程序或 API 服务。

装好后在侧栏选中「网易云音乐 Plus」，点 **登录**。

插件 id 是 `netease-cloud-music-plus`，和上游插件不同，两个可以同时装着、在侧栏切换对比。代价是登录态不共用：插件数据按 id 存放，要重新扫码登录一次。

## 登录

默认用网易云音乐 App 扫码，并在手机上确认。扫码不可用时，在插件设置里把 **登录方式** 设为 `web`，在弹出的窗口里登录。

登录态明文保存在宿主的插件数据文件里，不在系统钥匙串；cookie 只发给 `music.163.com` 和 `interfacepc.music.163.com`。退出登录会清掉本地登录态，并尝试同时结束网易云那边的会话。

## 与上游插件的三处不同

这个插件基于 [AkinoKaede 的插件](https://github.com/AkinoKaede/mygo-music-netease-cloud-music)，后者把这个客户端的网易云代码移植成了插件。改了三处，让行为与客户端本体一致：

1. **《我喜欢的音乐》出现在「我的歌单」里**，和客户端本体一样，而不是被藏起来。它在「收藏的歌单」里会被当成别人的歌单并提供「取消收藏」，所以不能放那边。
2. **侧栏不再单列「喜欢的音乐」**。它已经是「我的歌单」里的第一个歌单，和客户端本体的侧栏一样，不必有两个入口。
3. **每日推荐只有一个入口**：发现音乐首屏的每日推荐卡片。侧栏的「每日推荐」条目去掉了——它打开的是另一种版面的页面，和卡片点开的不是同一个。

第 3 条在旧版宿主上仍有差别：卡片打开的页面由宿主画（封面 + 标题 + 曲目数 + 播放/随机），没有日期封面、「每日推荐」小标和那一行推荐说明。插件已经把这三样放在 `home` 返回的 section 里（`kicker` / `pageTitle` / `subtitle` / `hero` 四个可选字段），宿主支持后自动生效，插件不用再改。

## 功能

- 未登录：推荐歌单、排行榜、搜索、专辑、歌手、公开歌单、播客发现、评论、歌词
- 已登录：每日推荐、我的歌单（含《我喜欢的音乐》）、歌单编辑、喜欢歌曲、收藏专辑、关注歌手、订阅播客、最近播放、私人 FM 与心动模式
- 评论：读、点赞、发表；精彩评论在 **探索** 里
- 不支持：视频播放、图片浏览、私人 FM 的「不感兴趣」

**为你推荐** 把每日推荐、今日为你推荐（登录后）、官方榜单和推荐歌单放在一页；**我的主页** 里有你的歌单、播客订阅、关注歌手、收藏专辑和最近播放；**探索** 里有歌手的新歌、专辑和精彩评论。

## 播放与歌词

音频直接从网易云串流，会员、购买与地区限制照旧生效；试听片段不会被当作完整歌曲播放。

**音质覆盖** 留空表示跟随播放器，也可填 `standard` / `higher` / `exhigh` / `lossless` / `hires`；实际能拿到哪一档取决于账号和录音。

逐字歌词与翻译优先用网易云的（YRC），没有时退回逐行歌词。播客转写由 MyGo Music 自己完成。

## 已知限制

- 《我喜欢的音乐》是网易云的固定歌单：不能改名、删除或拖动排序，点这些菜单会说明原因。喜欢一首歌就是把它加进去。
- 在这个歌单页里点爱心后，列表要重新进入页面才更新（宿主没有「歌单变了」的通知）。
- 歌曲菜单的「添加到歌单」里也会列出《我喜欢的音乐》，点它同样会说明原因而不是静默失败。

## 语言

跟随 MyGo Music 的语言设置：中文或英文。歌曲名、评论等网易云内容保持原语言。

## 致谢

- [MyGo Music](https://github.com/egoist/mygo-music)：插件运行环境
- [mygo-cloudmusic](https://github.com/Arteiimis/mygo-cloudmusic)：网易云接口、eapi 加密、扫码登录、歌单编辑的原始实现
- [AkinoKaede/mygo-music-netease-cloud-music](https://github.com/AkinoKaede/mygo-music-netease-cloud-music)：本插件的直接基础
- [NeteaseCloudMusicApi](https://github.com/Binaryify/NeteaseCloudMusicApi)：eapi 与登录流程的参考

## 许可

GNU Affero General Public License v3 或更高版本（`AGPL-3.0-or-later`）。完整文本见 [LICENSE](LICENSE)。
