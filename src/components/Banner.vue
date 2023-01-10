<template>
  <div id="banner">
    <h1>Monte Seu Hamburguer</h1>
  </div>
</template>

<script>
  export default {
    name: "Banner"
  }
</script>

<style scoped>

#banner {
  background-image: url('/public/img/burger.jpg');
  background-position: 0 -250px;
  background-size: cover;
  height: 500px;
  display: flex;
  align-content: center;
  justify-content: flex-start;
}

#banner h1 {
  color: #FFF;
  text-align: center;
  font-size: 60px;
  margin: auto;
  margin-left: 0;
  padding: 20px 30px; 
  background-color: #222;
}
</style>