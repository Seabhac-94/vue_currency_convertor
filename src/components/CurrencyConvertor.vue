<template>
    <h1>{{ msg }}</h1>
    <div>
      <h3>Base Currency: {{ baseCurrency }}</h3>
      <div>
          <p>
            <label for="userInputCurrencyCode">Currency Code </label>
            <input name="userInputCurrencyCode" type="text" v-model="userInputCurrencyCode">
          </p>
          <p>
            <label for="userInputAmount">Amount </label>
            <input name="userInputAmount" type="text" v-model="userInputAmount">
          </p>
          <button @click="getSelectedRate()">Convert</button>
          <p>{{userInputAmount}} {{userInputCurrencyCode}} is {{ result }} {{baseCurrency}}</p>
      </div>
    </div>

</template>

<script>
import axios from 'axios'

export default {
  name: 'CurrencyConvertor',
  props: {
    msg: String,
  },
  data(){
    return {
      apiEndpoint: "http://api.exchangeratesapi.io/v1/latest?access_key=7d16f262614ade1acdd720850c47bfae",
      info: null,
      baseCurrency: "",
      rates: null,
      userInputCurrencyCode: "",
      userInputAmount: null,
      currencyCode: null,
      rateOfCurrency: null,
      result: null
    }
  },
  mounted(){
    axios.get(this.apiEndpoint)
      .then(response => {
        this.info = response.data
        this.baseCurrency = this.info.base
        this.rates = this.info.rates
      })
  },
  methods:{
    getSelectedRate(){
        for (const cCode in this.rates) {
          if (this.userInputCurrencyCode.toUpperCase() === cCode && Object.hasOwnProperty.call(this.rates, cCode)) {
              this.currencyCode = cCode,
              this.rateOfCurrency = this.rates[cCode]
              // this.result = this.userInputAmount * this.rateOfCurrency
              this.result = this.userInputAmount / this.rateOfCurrency
              this.result = this.result.toFixed(2)
              break
              }
          else {
            console.log("Searching...")
          }
      }
      console.log(this.currencyCode + ' ' + this.rateOfCurrency)
    },
  },
  computed: {

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
