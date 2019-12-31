<template>
  <div class="hello">
    <h2>Currency Converter</h2>
    <div class="main-currency">
        <label for="currency">Euro:</label>
        <input type="text" id="euro" v-model="euro" >
    </div>
    <form>
      <!-- <div class="currency-box" v-for="(cur, index) in currencies" :key="index"> -->
      <div class="currency-box">
        <label for="currency">Dollar:</label>
        <input type="text" id="dollar" placeholder="current" :value="current">
        <button @click="convertedCur()">Convert</button>
      </div>
      <div class="currency-box">
        <label for="currency">Yen:</label>
        <input type="text" id="yen" :value="0">
        <button @click="convertedCur()">Convert</button>
      </div>
      <div class="currency-box">
        <label for="currency">Pounds:</label>
        <input type="text" id="pounds" :value="0">
        <button @click="convertedCur()">Convert</button>
      </div>
      <div class="currency-box">
        <label for="currency">Zloty</label>
        <input type="text" id="zloty" :value="0">
        <button @click="convertedCur()">Convert</button>
      </div>
      <div class="currency-box">
        <label for="currency">Real</label>
        <input type="text" id="real" :value="0">
        <button @click="convertedCur()">Convert</button>
      </div>
    </form>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  id: 'HelloWorld',
  data () {
    return {
      currencies: {},
      current: 0,
      euro: 0
    }
  },
  mounted() {
    axios.get('http://127.0.0.1:2000/currency')
    .then((response) => {
      this.currencies = response.data;
      console.log(response.data);
    }).catch((err) => {
      console.log(err);
    })

  },
  methods: {
    convertedCur() {
      let dollar = document.getElementById('dollar').value;
      this.current = dollar * euro;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.hello {
  width: 900px;
  text-align: center;
}
.main-currency {
  display: flex;
  justify-content: space-between;
  max-width: 200px;
  margin: 15px auto;
}
.main-currency label {
  font-size: 24px;
}
.main-currency input {
  width: 130px;
}
form {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.currency-box {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 270px;
  margin: 0 15px 15px;
}

.currency-box span {
  font-size: 12px;
  color: red;
}

.currency-box label {
  width: 40px;
}

.currency-box input {
  width: 100px;
}
</style>
