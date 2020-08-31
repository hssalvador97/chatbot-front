<template>
  <div id="app">
    <div class="container-fluid">
    <div class="row">
      <div class="col-md-6">
        <EjercicioComponent/>
      </div>
      <div class="col-md-6">
        <ChatComponent/>
      </div>
    </div>
    </div>
    
  </div>
</template>

<script>

import ChatComponent from './components/ChatComponent.vue'; 
import EjercicioComponent from './components/EjercicioComponent.vue'; 

export default {
  name: 'App',
  components: {
    ChatComponent, 
    EjercicioComponent

  }, 
}
</script>

<!--scoped para solo este componente-->
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
