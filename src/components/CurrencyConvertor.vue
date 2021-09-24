<template>
    <h1>{{ msg }}</h1>
    <button>Testing response</button>
    <div>
      <h3>Base Currency: {{ baseCurrency }}</h3>
      <div>
          <!-- <label for="currency">Choose a currency: </label>
          <select id="currency_select" name="currency">
            <option v-for="(key, value) in rates" :key="key">{{value}}</option>
          </select> -->
          <!-- <select id="currency_select" name="currency">
            <option>{{selectedCurrencyCode}}</option>
          </select> -->
          <p>
            <label for="userInputCurrencyCode">Currency Code </label>
            <input name="userInputCurrencyCode" type="text" v-model="userInputCurrencyCode">
          </p>
          <p>
            <label for="userInputCurrency">Amount </label>
            <input name="userInputCurrency" type="text" v-model="userInputCurrency">
          </p>
          <button @click="getSelectedRate()">Convert</button>
          <p>{{ result }}</p>
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
      userInputCurrencyCode: null,
      userInputCurrency: null,
      listOfCurrencyCodes: [],
      listOfRates: [],
      currencyCode: null,
      currency: null,
      result: null
    }
  },
  mounted(){
    axios.get(this.apiEndpoint)
      .then(response => {
        this.info = response.data
        this.baseCurrency = this.info.base
        this.rates = this.info.rates
        for (const key in this.rates) {
          if (Object.hasOwnProperty.call(this.rates, key)) {
            this.currencyCode = key,
            // this.listOfCurrencyCodes.push(this.currencyCode),
            // console.log(this.listOfCurrencyCodes)
            this.currency = this.rates[key]
            // console.log(this.currencyCode + ' ' + this.currency)
          }
      } 
      })
  },
  methods:{
    // getSelectedRate(){
    //   if (this.listOfCurrencyCodes.includes(this.userInputCurrencyCode)) {
    //     console.log(this.userInputCurrencyCode)
        
    //   } else {
    //     console.log("error")
    //   }
    // },
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
