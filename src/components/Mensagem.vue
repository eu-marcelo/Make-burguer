<template>
  <div class="mensagem-container">
    <P> {{ msg }} </P>
  </div>

</template>

<script>
export default {
  name: "Mensagem",
  props: {
    msg : String
  }
}
</script>

<style scoped>

.mensagem-container {
  color: #004085;
  background-color: #CCE5FF;
  border: 2px solid #88DAFF;
  border-radius: 5px;
  padding: 10px;
  max-width: 400px;
  margin: 30px auto;
}

</style>