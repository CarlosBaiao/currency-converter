<template>
  <div id="app">
    <Header/>
    <CurrencyType/>
    
    
  </div>
</template>

<script>
import Header  from "./components/Header.vue";
import CurrencyType  from "./components/CurrencyType.vue";


export default {
  name: 'App',
  components: {
   Header,
   CurrencyType,
   
  }
}
</script>

<style>
#app {
}
</style>
