<template>
  <div class="main-style">
  <p>hello</p>
  {{currencies}}
  <!-- {{data}} -->
  <div class="converter-wrapper">
    <div class="vselect">
        <v-select class="dropdown" placeholder="Base Currency:" v-model="base" :options="currencies"  />
        <v-select class="dropdown" placeholder="Target Currency:" v-model="target" :options="currencies"  />
        <form v-on:submit.prevent="submitForm">
          <!-- <br>
          <h2>Handle:</h2>
          <br>
          <div class="form-group">
              <input type="text" class="form-control" id="handle" placeholder="" v-model="form.handle">
          </div> -->
          <input type="submit" value="Convert!">
        </form>
      </div>
    </div>
    <!-- {{target}} -->
    <h1 v-if="display_target != display_base">1 {{display_base}} = {{data['data'][display_target]}} {{display_target}}</h1>
    <h1 v-else>convert to get results</h1>
  </div>
</template>

<script>

export default {
  name: 'App',
  components: {
    
  },
  data() {
    return {
      data: {},
      currencies: [ "USD", "JPY", "CNY", "CHF", "CAD", "MXN", "INR", "BRL", "RUB", "KRW", "IDR", "TRY", "SAR", "SEK", "NGN", "PLN", "ARS", "NOK", "TWD", "IRR", "AED", "COP", "THB", "ZAR", "DKK", "MYR", "SGD", "ILS", "HKD", "EGP", "PHP", "CLP", "PKR", "IQD", "DZD", "KZT", "QAR", "CZK", "PEN", "RON", "VND", "BDT", "HUF", "UAH", "AOA", "MAD", "OMR", "CUC", "BYR", "AZN", "LKR", "SDG", "SYP", "MMK", "DOP", "UZS", "KES", "GTQ", "URY", "HRV", "MOP", "ETB", "CRC", "TZS", "TMT", "TND", "PAB", "LBP", "RSD", "LYD", "GHS", "YER", "BOB", "BHD", "CDF", "PYG", "UGX", "SVC", "TTD", "AFN", "NPR", "HNL", "BIH", "BND", "ISK", "KHR", "GEL", "MZN", "BWP", "PGK", "JMD", "XAF", "NAD", "ALL", "SSP", "MUR", "MNT", "NIO", "LAK", "MKD", "AMD", "MGA", "XPF", "TJS", "HTG", "BSD", "MDL", "RWF", "KGS", "GNF", "SRD", "SLL", "XOF", "MWK", "FJD", "ERN", "SZL", "GYD", "BIF", "KYD", "MVR", "LSL", "LRD", "CVE", "DJF", "SCR", "SOS", "GMD", "KMF", "STD", "BTC", "XRP", "AUD", "BGN", "JOD", "GBP", "ETH", "EUR", "LTC", "NZD" ],
      prev_base: "",
      base : "",
      target: "",
      display_base: "",
      display_target: "",
    };
  },
  methods: {
    fetchData() {
      fetch(`https://freecurrencyapi.net/api/v2/latest?apikey=${process.env.VUE_APP_API_KEY}&base_currency=${this.base}`)
      .then((response) => response.json())
      .then((data) => {
        this.data = data;
        console.log("Fetching data...")
        // this.currencies = Object.keys(this.data.data);
      })
      .catch(error => {
        console.error(error);
      })
    },
    submitForm() {
      if (!this.base && !this.target) {
        alert("Please enter a base and a target");
      }
      else if (!this.base) {
        alert("Please enter a base");
      }
      else if (!this.target) {
        alert("Please enter a target");
      }
      else {
        if (this.base != this.prev_base) {
          this.fetchData();
        }
        this.prev_base = this.base; // keep track of previous base currency to minimize API calls
        this.display_base = this.base;
        this.display_target = this.target;
      }
    },
  },
  created() {
    this.fetchData();
  }
}
</script>

<style>

.main-style {
  --vs-controls-color: #664cc3;
  --vs-border-color: #664cc3;

  --vs-dropdown-bg: #282c34;
  --vs-dropdown-color: #cc99cd;
  --vs-dropdown-option-color: #cc99cd;

  --vs-selected-bg: #664cc3;
  --vs-selected-color: #201d1d;

  --vs-search-input-color: #eeeeee;

  --vs-dropdown-option--active-bg: #664cc3;
  --vs-dropdown-option--active-color: #eeeeee;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.dropdown {
  /* max-width: 50%; */
  position: relative;
  display: inline-block;
}

</style>
