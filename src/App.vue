<template>
  <div class="main-style">
  <p>hello</p>
  {{currencies}}
  <div class="vselect">
      <v-select class="dropdown" placeholder="Base Currency:" v-model="option" :options="currencies"  />
      <!-- <form v-on:submit.prevent="submitForm">
        <br>
        <h2>Handle:</h2>
        <br>
        <div class="form-group">
            <input type="text" class="form-control" id="handle" placeholder="" v-model="form.handle">
        </div>
        <input type="submit" value="submit">
      </form> -->
    </div>
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
      currencies: {},
      base : "BTC",
      option: "USD",
    };
  },
  methods: {
    fetchData() {
      fetch(`https://freecurrencyapi.net/api/v2/latest?apikey=${process.env.VUE_APP_API_KEY}&base_currency=${this.base}`)
      .then((response) => response.json())
      .then((data) => {
        this.data = data;
        this.currencies = Object.keys(this.data.data);
      })
      .catch(error => {
        console.error(error);
      })
    }
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
  --vs-selected-color: #eeeeee;

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
</style>
