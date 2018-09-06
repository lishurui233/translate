<template>
  <div id="app">
    <h1>在线翻译</h1>
    <h5 class="text-muted">简单 / 易用 / 便捷</h5>
    <translateForm v-on:form="translateText"></translateForm>
    <translateOutput v-text="translatedText"></translateOutput>

  </div>
</template>

<script>
import translateForm from './components/TranslateForm'
import translateOutput from './components/TranslateOutput'

export default {
  name: 'App',
  data(){
    return{
      translatedText:""
    }
  },
  components:{
    translateForm,
    translateOutput
  },
  methods:{
    translateText(text,language){
      //text是形参，用来接收translateText发送过来的Text
      // alert(text)
      this.$http.get('https://translate.yandex.net/api/v1.5/tr.json/translate?key=trnsl.1.1.20180905T142630Z.5b56e6026141c486.ad34d2f15c487fdecbff9388023afa8baebc5acf&lang='+language+'&text='+text)
      .then((res)=>{
        // console.log(res.body.text[0]);
        this.translatedText = res.body.text[0];
      })
    }

  }
}
</script>

<style>
  #app{
    font-family: 'Avenir',Arial, Helvetica, sans-serif;
    -webkit-font-smoothing:antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
</style>
