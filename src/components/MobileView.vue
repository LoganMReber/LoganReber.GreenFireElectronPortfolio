<template>
 <nav>
  <div>QR Codes</div>
  <div>Twitter</div>
 </nav>
</template>

<script>
  export default {
    name:"MobileView",
    data() {
      return {}
    }
  }
</script>

<style>
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

@media screen and (min-width: 721px){
  nav {
    display: none;
  }
}
</style>