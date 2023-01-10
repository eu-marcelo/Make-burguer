<template>
  <Navbar :logo="logo_src" :alt="nome_projeto"/>
  
  <router-view/>
  <Footer/>
</template>

<script>
import Navbar from './components/Navbar.vue'
import Footer from './components/Footer.vue'

export default  {
  components: {
    Navbar,
    Footer,
  },
  data() {
    return {
      logo_src: "./img/logo.png",
      nome_projeto: "Monte seu Lanche"
    }
  }
}
</script>


<style>
* {
  font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

.main-container {
  margin: 50px;
  min-height: 300px;
}

h1 {
  text-align: center;
  font-size: 42px;
  margin-bottom: 30px;
  color: #222;
}

</style>
