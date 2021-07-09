<template>
  <button v-on:click='save'>Save</button>
  {{imageURL}}
  <MobileView></MobileView>
  <div class='MainView'>
    <div class='feed'>
      <a 
        class="twitter-timeline" 
        data-lang="en" 
        data-width="300"
        data-height="700" 
        href="https://twitter.com/BBCAfrica?ref_src=twsrc%5Etfw"></a>
    </div>
    <Codes class='codes-component' v-if='data[0]' v-bind:data='data'></Codes>
    <div class='feed'>
      <a 
        class="twitter-timeline"
        data-lang="en" 
        data-width="300" 
        data-height="700" 
        href="https://twitter.com/ethereum?ref_src=twsrc%5Etfw"></a>
    </div>
  </div>
  <footer>
      <a href="https://github.com/LoganMReber/">Github</a>
      <a href="https://www.linkedin.com/in/logan-reber/">LinkedIn</a>
      <a href="/Logan_Reber_Resume">Resume</a>
      <a href="mailto: loganmreber@gmail.com">Email</a>
  </footer>
</template>

<script>
import axios from 'axios'
import html2canvas from 'html2canvas'
import MobileView from './components/MobileView.vue'
import Codes from './components/Codes.vue'
export default {
  name: 'App',
  components: {Codes,MobileView},
  data() {
    return {
      imageURL: '',
      res: null,
      data: [null,null,null],
      viewTab: 0
      }
  },
  methods:{
    save() {
      html2canvas(document.querySelector('.codes-component')).then( canvas => {
          this.imageURL = canvas.toDataURL('image/png')
          this.dlfile(this.imageURL,'Screenshot')
        });
    },
    dlfile(downloadUrl, downloadName) {
      let aLink = document.createElement("a");
      aLink.style.display = "none";
      aLink.href = downloadUrl;
      aLink.download = `${downloadName}.png`;
      document.body.appendChild(aLink);
      aLink.click();
      document.body.removeChild(aLink);
    }
  },
  watch: {
    imageURL: function(){
      window.open(this.imageURL)
      }
  },
  mounted() {
    let scr = document.createElement('script')
    scr.setAttribute('src',"https://platform.twitter.com/widgets.js")
    scr.setAttribute('async',true)
    document.head.appendChild(scr)
    axios.get('https://api.coingecko.com/api/v3/simple/price?ids=tezos%2Calgorand%2Csignum&vs_currencies=usd')
      .then(res => {
        this.res = res,
        this.data[0] = "Tezos - " + res.data.tezos.usd + " USD"
        this.data[1] = "Burst - " + res.data.signum.usd + " USD"
        this.data[2] = "Algorand - " + res.data.algorand.usd + " USD"
        })
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

footer {
 display:flex;
 flex-direction:column;
}
footer a {
 color:#FFF;
 background-color:#000;
 text-decoration:none;
 margin-top: 1px;
 font-size: 24px;
 padding: 10px 0px;
}
footer a:hover {
 background-color:#333;
}
.MainView {
  display: flex;
  justify-content:space-between;
}
.feed {
  min-width:300px;
  }
@media screen and (max-width: 800px){
  .MainView {
    display: none;
  }
}

</style>
