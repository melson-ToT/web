
安装依赖

npm i --save flv.js


组件使用
import flvjs from 'flv.js'


<template>  
<video
  id="videoElement"
  ref="videoElement"
  controls
  muted
  width="100%"
  height="100%"
></video>
<template> 

<script>
data() {
  return {
    flvPlayer: null
  }
},
methods: {
  //创建flv视频实例
  createFlv() {
    let url="http://xxxxxxxx.flv";
    if (flvjs.isSupported()) {
     let videoElement = document.getElementById("videoElement");
     this.flvPlayer = flvjs.createPlayer({
       type: "flv",// 媒体类型，默认是 flv,
       isLive: true,// 是否是直播流
       hasAudio: false,// 是否有音频
       hanVideo: ture, // 是否有视频
       url
     });
     this.flvPlayer.attachMediaElement(videoElement);
     this.flvPlayer.load();
    }
  }
}
4.销毁flv实例
//销毁flv实例
flv_destroy() {
  if (this.flvPlayer) {
    this.flvPlayer.pause();
    this.flvPlayer.unload();
    this.flvPlayer.detachMediaElement();
    this.flvPlayer.destroy();
    this.flvPlayer = null;
  }
}
</script>





flv 同时支持 WebSocket 和 HTTP 两种传输方式, 在 web 端，我们使用功能 flv.js 来处理 flv 格式的直播流 官网链接
安装依赖 npm install --save flv.js

<template>
  <div>
    <video autoplay controls width="100%" height="500" id="myVideo"></video>
  </div>
</template>

<script>
import flvjs from 'flv.js'

// 检测浏览器是否支持 flv.js
createdPlay() {
  if (flvjs.isSupported()) {
    var videoDom = document.getElementById('myVideo')
    // 创建一个播放器实例
    var player = flvjs.createPlayer({
      type: 'flv', // 媒体类型，默认是 flv,
      isLive: true, // 是否是直播流
      hasAudio: ture, // 是否有音频
      hanVideo: ture, // 是否有视频
      url: 'http://test.stream.com/fetch-media.flv'， // 流地址
    },{
      // 其他的配置项可以根据项目实际情况参考 api 去配置
      autoCleanupMinBackwardDuration: true, // 清除缓存 对 SourceBuffer 进行自动清理
    })
    player.attachMediaElement(videoDom)
    player.load()
    player.play()

    this.player = player
  }
}
在网络较好的情况下，这样子没啥大问题，那在网络不好的时候怎么办呢，有没有一些事件去处理这些异常呢，我们接着往下看

【音视频学习资料推荐】


处理异常
官网给出了处理异常的方法， flvjs.Events.Error

player.on(flvjs.Events.ERROR, (errType, errDetail) =>{
  // todo
}) 
errType: 错误类型
NETWORK_ERROR：网络错误
MEDIA_ERROR：媒体错误
OTHER_ERROR： 其他
errDetail: 错误详情，提供流的一些详细信息
NETWORK_STATUS_CODE_INVALID：HTTP 状态码错误
MEDIA_MSE_ERROR: 与 MediaSource 的错误有关，如解码问题
MEDIA_FORMAT_ERROR：媒体格式不支持
MEDIA_FORMAT_UNSUPPORTED：媒体格式不支持, 不是 flv 格式
NETWORK_TIMEOUT：连接超时
组件实例销毁

  destroyVideos(){
    if(!this.player) return
    this.player.pause()
    this.player.unload()
    this.player.detachMediaElement()
    this.player.destroy()
    this.player = null
  }
在播放的时候，可能会有卡顿的情况，这个时候我们需要重新去拉流这个时候怎么办呢 但是由于视频会延时，为保证实时性，我们可以跳帧

let timer = setInterval(() => {
  if (player.buffered && player.buffered.length) {
    let end = player.buffered.end(0); // 获取当前buffered值
    let diff = end - player.currentTime; // 获取buffered与currentTime的差值
    if (diff >= 60) {// 如果差值大于等于60s 手动跳帧 这里可根据自身需求来定
      //单个视频
      // player.currentTime = end;//手动跳帧
      // player.currentTime = player.buffered.end(0);//手动跳帧

      // 多个视频
      clearInterval(timer)
      player.pause();
      player.unload();
      player.detachMediaElement();
      player.destroy();
      player= null;
      //重新加载当前停止的视频流，根据个人的方法来配置
      this.createdPlay()
    }
  }
}, 2000); //2000毫秒执行一次
flv.js 还提供了一种事件 statistics_info 播放流的详细信息

this.player.on("statistics_info", (res) =>{
  if (this.lastDecodedFrame == 0) {
    this.lastDecodedFrame = res.decodedFrames;
    return;
  }
  if (this.lastDecodedFrame != res.decodedFrames) {
    this.lastDecodedFrame = res.decodedFrames;
  } else {
    this.lastDecodedFrame = 0;
    if (this.player) {
      this.reloadVideo()
    }
  }
})
延时的问题可以通过跳帧的方法解决，但是如果视频卡顿导致流断了，那就可以重连

this.player.on(flvjs.Events.ERROR, (errType, errDetail) =>{
  if(this.player){
    this.destroyVideos()
    this.createdPlay()
  }
})
其他异常错误
Uncaught (in promise) DOMException: play() failed because the user didn't interact with the document first.
方案：为 video 标签设置muted属性，静音自动播放，当用户触发点击行为时，再将 muted 属性置为 false，或者，让用户手动播放。
Uncaught (in promise) DOMException: The play() request was interrupted by a call to pause() 方案：在播放需要先执行暂停播放，可能是因为未加载完毕就已经开始播放了，手动点击播放就不会有这个问题，可以通过 flvjs.Events.METADATA_ARRIVED 这个方法获取视频是否加载完成
flv.js播放视频时出现Failed to execute ‘appendBuffer’ on ‘SourceBuffer’ 方案：这个是因为代码的一些业务逻辑导致的，可以参考下面两个例子去调试 www.cnblogs.com/melancholys… github.com/bilibili/fl…
关于 flv.js 播放的时候用户没有推音频报错的问题。
方案： 修改 src/demux/flv-demuxer.js 的方法

 set overridedHasAudio(hasAudio) {
    // this._hasAudioFlagOverrided = true;
    // this._hasAudio = hasAudio;
    // this._mediaInfo.hasAudio = hasAudio;
    
    this._hasAudioFlagOverrided = true;
    this._hasAudio = this.hasAudio? hasAudio: false;
    this._mediaInfo.hasAudio = this.hasAudio;
}
修改完之后，两种打包方式

npm run build:debug    # debug version flv.js will be emitted to /dist
npm run build          # minimized release version flv.min.js will be emitted to /dist
我使用的是npm run build引入的时候方式有所改变




作者:吴小白菜

原文链接：https://ffmpeg.0voice.com/forum.php?mod=viewthread&tid=1190

