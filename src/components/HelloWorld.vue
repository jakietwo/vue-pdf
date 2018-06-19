<template>
  <div>
    <div>
      <div v-if="isload">loading</div>
      <pdf ref="myPdfComponent" v-show="!isload"
           src="https://cdn.mozilla.net/pdfjs/tracemonkey.pdf"
           :page="page"
           @loaded="loaded"
           @num-pages="pageCount = $event"
           @page-loaded="currentPage = $event"
      ></pdf>

      {{currentPage}} / {{pageCount}}
      <button style="position: absolute;z-index: 10" @click="back">上一页</button>

      <button @click="$refs.myPdfComponent.print()">print</button>
      <button @click="next" style="position: absolute;z-index: 10">下一页</button>
    </div>
  </div>


</template>

<script>
  import pdf from 'vue-pdf'

  var loadingTask = pdf.createLoadingTask('./../../static/1.pdf');
  import vueshowpdf from 'vueshowpdf'

  export default {
    name: 'HelloWorld',
    data() {
      return {
        msg: 'Welcome to Your Vue.js App',
        currentPage: 0,
        pageCount: 0,
        page: 1,
        src: loadingTask,
        numPages: undefined,
        isload: true
      }
    },
    components: {
      pdf
    },
    mounted() {

    },
    methods: {
      next() {
        if (this.page < this.pageCount) {
          this.page++;
        }
      },
      back() {
        if (this.page>1){
          this.page--;
        }
      },
      loaded(){
        this.isload = false;
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
