<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    
    <p v-text="busy"></p>
    <p v-text="sale"></p>
    <input v-model="search" type="text" placeholder="id producto">
    <ul v-if="searchById">
      <li>{{searchById.nombre}}</li>
    </ul>
    <ul v-else>
      <li v-for="(product, index) in availableProducts" :key="index">{{product.nombre}}</li>
    </ul>

    <p>Ofertas</p>
     <ul>
      <li v-for="(product, index) in cheapProducts" :key="index">{{product.nombre}} {{product.precio}}</li>
    </ul>
  </div>
</template>

<script>

import {mapState, mapGetters} from 'vuex'; //mapaState ayudador que permite importar partes del store para acceder a las variables 

export default {
  name: 'App', 
  data(){
    return{
      search: null
    }
  },
  computed:{ 
    ...mapState(['isBusy', 'sales']), /**se llaman las variables desde store.js */
    ...mapGetters(['availableProducts', 'cheapProducts', 'getProductById']),
    

    busy(){
      /* store constante iniciada en store.js state viene del store.js */
      let status = this.isBusy ? 'Ocupado' : 'Disponible' 
      return `Estado ${status}`
    },
    sale(){
      /* primer $ para interpolar una variable (para decir que va a ver ua variable dentro de un string)*/
      return `el total de ventas es: ${this.sales}`
    },
    searchById () {
      return this.getProductById(this.search)
    }
  },
}
</script>

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
