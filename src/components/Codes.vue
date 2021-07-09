<template>
  <div class="codes">
    <div class="code">
      <h3>Logan Reber</h3>
      <vue-qr margin='0' size='100' text="Logan Reber"></vue-qr>
    </div>
    <div class="code">
      <h3>{{data[0]}}</h3>
      <vue-qr margin='0' size='100' :logoSrc='logo1' :text="data[0]"></vue-qr>
    </div>
    <div class="code">
      <h3>{{data[1]}}</h3>
      <vue-qr margin='0' size='100' :logoSrc='logo2' :text="data[1]"></vue-qr>
    </div>
    <div class="code">
      <h3>{{data[2]}}</h3>
      <vue-qr margin='0' size='100' :logoSrc='logo3' :text="data[2]"></vue-qr>
    </div>
  </div>
</template>
<script>
  import VueQr from 'vue-qr/src/packages/vue-qr.vue'
  export default {
    name: 'Codes',
    components: {VueQr},
    props: {
      data: Array
      },
    data() { 
      return {
        logo1:"./tezos.png",
        logo2:"./burstcoin.png",
        logo3:"./algorand.png"  
      }
    }
  }
  
</script>

<style>
.codes {
  display:flex;
  flex-wrap:wrap;
  justify-content: space-evenly;
  align-items:center;
}
@media screen and (max-width:800px){
  .codes {
    width: 100%;
  }

}
.code {
  /* display: flex; */
  flex-direction:column;
  align-items:center;
  width: 140px;
}
.code h3 {
height: 30px;
display:flex;
  justify-content: center;
  align-items: center;
}
</style>