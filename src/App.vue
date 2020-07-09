<template>
  <div id="app">
    <div class="field">
      Cadastro de Produtos
    </div>
    <div id="form">
      <Login/>
    </div>
  </div>
</template>

<script>
import Login from './components/Login.vue';

export default {
  name: 'App',
  components:{
    Login
  }
}
</script>


<style>
  html{
    background: rgb(0,0,0);
    background: linear-gradient(90deg, rgba(0,0,0,1) 0%, rgba(40,40,55,1) 45%, rgba(136,136,136,1) 100%);
  }

  #field{
    width: 100%;
  }

  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: white;
    margin-top: 35vh;
  }

  #form{
    margin-top:5vh;
  }
</style>
