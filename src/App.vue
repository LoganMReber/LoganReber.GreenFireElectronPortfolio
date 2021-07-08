<template>
  <Codes v-if='data[0]' v-bind:data='data'></Codes>
  <a
      class="twitter-timeline"
       data-lang="en" data-width="300" data-height="540" 
      href="https://twitter.com/ethereum?ref_src=twsrc%5Etfw"
      >Tweets by ethereum</a
    >
</template>

<script>
import axios from 'axios'
import Codes from './Codes.vue'
export default {
name: 'App',
  components: {Codes},
  data() {
    return {
      res: null,
      data: [null,null,null]
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

</style>
