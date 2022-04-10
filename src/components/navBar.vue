<template>
  <header class="header">
    <img src="https://www.construya.com/images/inicio/logo_horizontal.png" alt="logo" class="logo" />
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
  justify-content: center;
  height: 80px;
  left: 0;
  position: relative;
  top: 0;
  width: 100%;
  z-index: 99;
  border-bottom: 1px solid transparent;
  transition: 0.3s;
  background-color: #eff7ff;
}

</style>