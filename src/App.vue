<template>
  <div id="app">
    <h1>Conversão de moedas</h1>
    <div class="moeda">
      <converter />
    </div>
  </div>
</template>

<script>
import Converter from './components/converter.vue'
export default {
  name: 'App',
  components: {
    Converter
  }
}
</script>

<style>
h1 {
    text-align: center;
}

.moeda {
    display: flex;
    justify-content: space-around;
    margin: auto;
    max-width: 800px;
    text-align: center;
}

.conversao {
    border: solid 1px;
    max-width: 300px;
    margin-top: 20px;
    padding: 10px;
    border-radius: 7px;
}

select {
  margin: auto 20px;
}

.troca {
    padding: 0 20px;
}

.select {
  margin: 10px;
}
</style>