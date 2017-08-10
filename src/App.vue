<template>
  <div id="app">
    <img src="./assets/logo.png" @click="tab">
    <router-view></router-view>
  </div>
</template>

<script>
export default {
  name: 'app',
  methods:{
    tab(){
      var cmr = plus.camera.getCamera();
      cmr.captureImage( function ( p ) {
        //成功
        plus.io.resolveLocalFileSystemURL( p, function ( entry ) {

          var img_name = entry.name;//获得图片名称
          var img_path = entry.toLocalURL();//获得图片路径

        }, function ( e ) {
          console.log( "读取拍照文件错误："+e.message );
        } );

      }, function ( e ) {
        console.log( "失败："+e.message );
      }, {filename:'_doc/camera/',index:1} ); //  “_doc/camera/“  为保存文件名
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
