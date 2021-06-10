# 方案评估

## 填写评估表
我们为接入游戏提供了评估表，本文档用于阐述“评估表”中的事项以及项目在转换时可能遇到的问题，帮助项目组决定是否使用转换方案。

<image src='../image/evaluation1.png' width="200"/>


## 需要注意的事项
### 1、关于游戏类目
考虑到游戏体积与逻辑复杂度，目前建议中轻度2D/3D游戏进行转换，游戏类目包括：
* 休闲：消除，答题，模拟经营，塔防，益智等
* 动作：跑酷，飞行设计，轻度IO
* 棋牌：棋类，牌类
* 角色：卡牌，回合，策略

对重度游戏如MMO/FPS等游戏需根据实际情况评估  


### 2. 关于引擎版本

本转换方案目前支持：
* Unity 2018
* Unity 2019
  
  其他版本在未来也可支持，如果开发者有其他版本需求可与我们联系。


### 3. 开发需要具备的技术栈
* 前端：开发者可以继续使用Unity，编程语言C#，微信平台能力以C# SDK提供
* 后台：通常短连接使用HTTPS接入，长连接使用WSS。也可选择使用小程序云作为后端服务。
* H5开发经验：无需专门的H5经验，但需要简单了解下微信小游戏开发流程与工具

### 4. Unity WebGL在小游戏与浏览器环境的运行差异
* Android/PC(Windows)：支持特性与浏览器一致，运行Unity WebGL的核心部分从性能上差别不大
* iOS：支持特性与浏览器一致，性能略低于Webview

建议开发者先将游戏导出为WebGL在浏览器上运行，如果没有严重的兼容性问题则可使用本方案。

### 5. 是否能使用第三方插件
可以，支持C#插件(有无源码均可)与C原生插件(需源码)

### 6. 渲染品质与还原度
在小游戏环境下，Unity WebGL导出格式的底层渲染特性支持WebGL 1.0(OpenGL ES2.0), 未来我们将支持2.0。WebGL 1.0的限制请查阅[WebGL 图形](https://docs.unity3d.com/cn/current/Manual/webgl-graphics.html).


### 7. 是否能使用热更
通常，app开发时大家会由于审核速度问题采用LUA/ILRuntime等热更方案。然而，在小游戏环境中不被允许。原因如下：
* 小游戏运营策略不允许动态变更代码，包括热更
* LUA/ILRuntime等热更方案在Unity WebGL性能急剧下降

### 8. 是否能使用物理引擎
可以，但由于Unity WebGL算力不如原生APP(约1/3)，因此建议避免使用较重的物理计算，可结合Fixed Timestep控制计算频率。

### 9. 是否能使用多线程
不可以，Unity WebGL是单线程模式。

### 10. 是否能使用协程
可以

### 11. 动画/Drawcall的限制
复杂的动画与Drawcall对严重消耗CPU资源，如问题6所述受算力影响，开发者需根据实际项目进行Profile。

### 12. 包体大小限制
建议APP端资源体积不超过300MB的游戏进行转换，原因如下：
* 小游戏资源缓存大小为200MB
* 过大的游戏造成的加载缓慢容易导致用户流失
在此前提下，建议开发者根据后续启动性能优化指引进行启动时长的调优


### 13. 资源分包
小游戏环境同时支持AssetsBundle与Addressable资源加载方式
由于完整打包一次性下载会导致启动时间过长，如果原生APP未进行资源异步加载，需要开发者进行改造优化。

### 14. Unity音频支持
目前Unity WebGL的音频虽然能完整支持，在性能与内存占用上还存在问题，建议开发者在使用小游戏提供的音频SDK进行替换。

### 15. 网络接口
* HTTP/WWW：已支持
* TCP: 需替换成Websocket
* UDP: 暂未支持，如果开发者有此需求与我们联系




 