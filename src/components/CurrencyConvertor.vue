<template>
    <h1>{{ msg }}</h1>
    <div>
      <h3>Base Currency: {{ baseCurrency }}</h3>
      <div >
          <p>
            <label for="userInputCurrencyCode">Currency Code </label>
            <input name="userInputCurrencyCode" type="text" v-model="userInputCurrencyCode"> <span v-if="currencyCodeIsNotValid">Currency Code not valid!</span>
          </p>
          <p>
            <label for="userInputAmount">Amount </label>
            <input name="userInputAmount" type="number" v-model="userInputAmount">
          </p>
          <button @click="getSelectedRate()">Convert</button>
          <p v-if="showResult">{{userInputAmount}} {{userInputCurrencyCode}} is {{ displayedResult }} {{baseCurrency}}</p>
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
      currencyCodeIsNotValid: null,
      rateOfCurrency: null,
      result: null,
      displayedResult: null,
      showResult: false
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
              this.displayedResult = this.result.toFixed(2)
              this.currencyCodeIsNotValid = false,
              this.showResult = true
              break
              }
          else{
            this.currencyCodeIsNotValid = true,
            this.currencyCode = null,
            this.rateOfCurrency = null
          }
      }
      console.log(this.currencyCode + ' ' + this.rateOfCurrency)
    },
  },
watch: {
  // result(value){
  //   if (value != this.userInputAmount / this.rateOfCurrency) {
  //     this.showResult = false
  //   } else {
  //     this.showResult = true
  //   }
  // }
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
