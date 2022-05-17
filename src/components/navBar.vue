<template>
  <header class="header">
    <img src="https://www.construya.com/images/inicio/logo_horizontal.png" alt="logo" class="logo" />
    <img src="../entreamigos.svg" alt="logo" class="logo" />
  </header>
</template>
<script>
export default {
  name: 'NavBar',
  data() {
    return {}
  },
  methods: {}
}
</script>
<style lang="scss">
.header {
  display: flex;
  justify-content: space-evenly;
  height: 136px;
  left: 0;
  position: relative;
  top: 0;
  width: 447px;
  z-index: 99;
  border-radius: 0px 0px 24px 0px;
  background: #FFFFFF;
  box-shadow: 0px 10px 18px rgb(9 30 66 / 15%), 0px 0px 1px rgb(9 30 66 / 31%);
  border-bottom: 1px solid transparent;
  transition: 0.3s;
  /* background-color: #eff7ff; */
  align-items: center;
  flex-wrap: wrap;
  justify-items: center;
  align-content: center;
}
@media(max-width: 768px){
  .header{
    border-radius: 0px 0px 16px 16px;
    width: 314px;
    height: 88px;
    padding-right: 0px;
  }
  .logo{
    max-width: 125px;
  }
  #app{
    place-items: center;
  }
}

</style>