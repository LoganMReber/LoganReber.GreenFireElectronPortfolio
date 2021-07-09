<template>
  <button v-on:click='save'>Download Data</button>
  <div class='MainView'>
  <Codes class='codes-component' v-if='data[0]' v-bind:data='data'></Codes>
    <div class='feed'>
      <a 
        class="twitter-timeline" 
        data-lang="en" 
        data-width="280"
        data-height="560"
        data-theme="dark"
        href="https://twitter.com/BBCAfrica?ref_src=twsrc%5Etfw"></a>
    </div>
    
    <div class='feed'>
      <a 
        class="twitter-timeline"
        data-lang="en" 
        data-width="280" 
        data-height="560"
        data-theme="dark"
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
import Codes from './components/Codes.vue'
export default {
  name: 'App',
  components: {Codes},
  data() {
    return {
      tab:0,
      width: window.innerWidth,
      imageURL: '',
      res: null,
      data: [null,null,null]
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
    },
    widthChange(){
      this.width = window.innerWidth
    }
  },
  watch: {
    imageURL: function(){
      window.open(this.imageURL)
      }
  },
  mounted() {

    //Twitter Embed Script
    let scr = document.createElement('script')
    scr.setAttribute('src',"https://platform.twitter.com/widgets.js")
    scr.setAttribute('async',true)
    document.head.appendChild(scr)

    //Crypto API retrieval
    axios.get('https://api.coingecko.com/api/v3/simple/price?ids=tezos%2Calgorand%2Csignum&vs_currencies=usd')
      .then(res => {
        this.res = res,
        this.data[0] = "Tezos - " + res.data.tezos.usd + " USD"
        this.data[1] = "Burst - " + res.data.signum.usd + " USD"
        this.data[2] = "Algorand - " + res.data.algorand.usd + " USD"
        })

    window.addEventListener('resize', this.widthChange)    
  },
  unmounted() {
    window.removeEventListener('resize', this.widthChange)
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  min-height: 100vh;
  display:flex;
  flex-direction:column;
  justify-content:space-between;
}
nav {
  display:flex;

}
nav div {
  width:50%;
  height:60px;
  display:flex;
  justify-content:center;
  align-items:center;
  color: #FFF;
  background-color: #000;
  font-size: 24px;
}
nav div:hover{
  background-color: #222;
}
nav div.active {
  background-color: #333;
}

@media screen and (min-width: 801px){
  nav {
    display: none;
  }
}
button {
  padding:10px 70px;
  color:#FFF;
  background-color:#000;
  border: none;
  margin: 5px;
  font-size: 24px;
}
button:hover{
  background-color:#333;
}

.MainView {
  display: flex;
  justify-content:center;
  flex-wrap:wrap;
}
.feed {
  min-width:300px;
  margin:10px;
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
</style>
