<script setup>
import Searcher from './components/searcher.vue'
</script>

<template>
  <div class="main-body">
    <header>

    </header>

    <main class="body-inner">
      <Searcher/>
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
  background-color: rgb(249, 249, 249);;
}

.wrapper {
  display: inline-block;
  height: 100%;
  width: 100%;
}

.main-body {
  max-width: 550px;
  margin: 10px auto;
  /*!* padding-top: 10%;*/
}
.body-inner{
  padding: 20px;
  padding-bottom: 0px;
}


#app {
  max-width: 1280px;
  margin: 0 auto;
  padding: 2rem;

  font-weight: normal;
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
  line-height: 2.1rem;
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
  border: 1px solid transparent;
  padding: 0.375rem 0.75rem;
  font-size: 1rem;
  line-height: 1.5;
  border-radius: 0.25rem;
  transition: color .15s ease-in-out,background-color .15s ease-in-out,border-color .15s ease-in-out,box-shadow .15s ease-in-out;
}
@media (hover: hover) {
  a:hover {
    background-color: hsla(160, 100%, 37%, 0.2);
  }
}

@media (min-width: 1024px) {
  body {
    display: flex;
    place-items: center;
    font-family: 'Roboto', sans-serif;
  }

  #app {
    display: grid;
    grid-template-columns: 1fr 1fr;
    padding: 0 2rem;
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
    margin: 0 2rem 0 0;
  }
}
</style>
