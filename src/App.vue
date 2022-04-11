<script setup>
import Searcher from './components/searcher.vue'
import NavBar from './components/navBar.vue'
</script>

<template>
  <NavBar>

  </NavBar>
  <div class="main-body">

    <main class="body-inner">
      <Searcher/>
      <img class="content-img" src="./construya-money.svg" />
    </main>
  </div>

</template>

<style lang="scss">
@import './assets/base.css';

body {
  margin: 0;
  padding: 0;
  height: 100%;
  position: relative;
  background-color: #c4d600;
  font-family: 'Montserrat', sans-serif;
}

.wrapper {
  display: inline-block;
  height: 100%;
  width: 100%;
}

.main-body {
  max-width: 75vw;
  margin: 10px auto;
  /*!* padding-top: 10%;*/
}
.body-inner{
  padding: 20px;
  padding-bottom: 0px;
  display: grid;
  grid-template-columns: 1.5fr 1fr;
  grid-template-areas: ". .";
  justify-content: space-evenly;
  justify-items: stretch;
  align-content: center;
  vertical-align: center;
  align-items: center;
}
.content-img{
  height: 80%;
}


#app {
  /*max-width: 1280px;*/
  /*margin: 0 auto;*/
  /*padding: 2rem;*/

  /*font-weight: normal;*/
  width: 100%;
  height: 100vh;
  margin: 0;
  padding: 0;
  height: 100%;
  position: relative;
  display: block;
  place-items: center;
  font-family: 'Montserrat', sans-serif;
}

header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

a,
.green {
  text-decoration: none;
  color: hsla(160, 100%, 37%, 1);
  transition: 0.4s;
}
h1{
  font-weight: bolder;
  line-height: 3.1rem;
  font-size: 3.5rem;
  color: white;
}
.btn{
  display: inline-block;

  text-align: center;
  white-space: nowrap;
  vertical-align: middle;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
  border: 0px solid transparent;
  padding: 0.375rem 0.75rem;
  font-size: 1rem;
  line-height: 1.5;
  border-radius: 0 0.25rem 0.25rem 0;
  transition: color 0.15s ease-in-out, background-color 0.15s ease-in-out, border-color 0.15s ease-in-out, box-shadow 0.15s ease-in-out;
}
@media (hover: hover) {
  a:hover {
    background-color: hsla(160, 100%, 37%, 0.2);
  }
}

@media (max-width: 1024px) {
  #app {
    /*display: flex;*/
    /*grid-template-columns: 1fr 1fr;*/
    justify-content: center;
    /*padding: 0 2rem;*/
  }

  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  .logo {
  }
  .selected{
    font-size:11px;
  }
  .main-body{
    max-width: 100vw;
  }
  .body-inner{
    padding: 20px 20px 0;
    display: block!important;
    grid-template-columns: 1fr!important;
    grid-template-areas: ". .";
    justify-content: flex-start;
    justify-items: stretch;
  }
  h1{
    line-height: 1.8rem;
    font-size: 1.5rem;
  }
}
</style>
