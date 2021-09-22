<template>
    <h1>{{ msg }}</h1>
    <div>
      <h3>Base Currency: {{ baseCurrency }}</h3>
      <button @click="getRates">click me</button>
      {{ info }}
    </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'CurrencyConvertor',
  props: {
    msg: String
  },
  data(){
    return {
      apiEndpoint: "http://api.exchangeratesapi.io/v1/latest?access_key=7d16f262614ade1acdd720850c47bfae",
      info: null,
      baseCurrency: ""
    }
  },
  mounted(){
    axios.get(this.apiEndpoint)
      .then(response => {
        this.info = response.data
        this.baseCurrency = this.info.base
      })
  },
  methods:{
    getRates() {
      const rates = this.info.rates
      console.log(Object.values(rates))
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
/* h3 {
  margin: 40px 0 0;
} */
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
