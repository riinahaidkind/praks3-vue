<template>
  <div> 
  <h1>Numbrifaktid</h1>
  <p>Huvitavad faktid iga numbri kohta</p>
  <input type="number" min="0" v-model="number">
  <input type="inkrement" min="0" v-model="inkrement">
    <p v-for="(item, index) in data" :key="index">{{ item }}</p>
    
  </div>
</template>

   // vaja saada sarnane URL
    // http://numbersapi.com/1..3
    
    
<script>
    const axios = require('axios')
    
export default {
  name: 'Faktid',
  data (){
      return {
        data: 0,
        number: 0,
        inkrement: 0,
        }
    },
    methods: {
        getResponse () {
            if (this.number !== '' && this.inkrement !== '') { 
                let baseUrl = 'http://numbersapi.com/'
                let url = `${baseUrl}${this.number}..${parseInt(this.number) + parseInt(this.inkrement)}`;
                
                axios.get(url)
                .then(response => {
                    this.data = response.data
                })
                .catch(error => {
                    console.log(error)
                })
            }
        }
    },
    watch: {
        number() {
            this.getResponse()
        },
        inkrement () {
            this.getResponse()
            
        }
            
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    
</style>
