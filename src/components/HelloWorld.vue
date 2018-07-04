<template>
  <div>

      <!--<div v-if="isload">loading</div>-->
      <!--<pdf ref="myPdfComponent" v-show="!isload"-->
           <!--src="https://cdn.mozilla.net/pdfjs/tracemonkey.pdf"-->
           <!--:page="page"-->
           <!--@loaded="loaded"-->
           <!--@num-pages="pageCount = $event"-->
           <!--@page-loaded="currentPage = $event"-->
      <!--&gt;</pdf>-->

      <!--{{currentPage}} / {{pageCount}}-->
      <!--<button style="position: absolute;z-index: 10" @click="back">上一页</button>-->

      <!--<button @click="$refs.myPdfComponent.print()">print</button>-->
      <!--<button @click="next" style="position: absolute;z-index: 10">下一页</button>-->

      <video autoplay height="375" width="350"> </video>

  </div>


</template>

<script>
  import adapter from 'webrtc-adapter'
  export default {
    name: 'HelloWorld',
    data() {
      return {
        msg: 'Welcome to Your Vue.js App',
        video: '',
        stream: '',
        peerConn:'',
        connecteduser: null,
        configuration: {
          iceServers:[
            {
              urls: "turn:115.28.170.217:3478",
              credential: "wjg",
              username: 'wjg'
            }
          ]
        }

      }
    },
    sockets:  {
      connect(){
        console.log('socket connect success!');
      }
    },
    components: {

    },
    mounted() {
      console.log(adapter.browserDetails.browser);
      this.video = document.querySelector('video');
      var constraints = window.constraints = {
        audio: true,
        video: true
      };
      navigator.mediaDevices.getUserMedia(constraints).then(this.handleSuccess).catch(this.handleError)
    },
    methods: {
      handleSuccess(stream) {
        let videoTracks = stream.getVideoTracks();
        console.log('using video device:' + videoTracks[0].label);
        this.video.srcObject = stream;
      },
      handleError(error){
        console.log('getUserMedia error:' + error.name, error)
      },

    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
