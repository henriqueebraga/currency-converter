<template>
  <div class="hello">
    <h2>Currency Converter</h2>
    <div class="main-currency">
        <label for="currency">Euro:</label>
        <input type="text" id="euro" v-model="euro" >
    </div>
    <div class="row">
        <div id="checkboxes">
            <label>Dollar</label>
            <input type="checkbox" id="dollar" value="dollar" name="current-currency" @click="convertCurrency" v-model="data.categories" />
        </div>
        <div id="checkboxes">
            <label>Yen</label>
            <input type="checkbox" id="yen" value="yen" name="current-currency" @click="convertCurrency" v-model="data.categories" />
        </div>
        <div id="checkboxes">
            <label>Pounds</label>
            <input type="checkbox" value="pounds" name="current-currency" v-model="data.categories" />
        </div>
        <div id="checkboxes">
            <label>Zloty</label>
            <input type="checkbox" value="zloty" name="current-currency" v-model="data.categories" />
        </div>
        <div id="checkboxes">
            <label>Real</label>
            <input type="checkbox" value="real" name="current-currency" v-model="data.categories" />
        </div>
    </div>    
    <ul>
        <li id="dollar-result">Your conversion for dollar is {{  }}</li>
        <li id="yen-result">Your conversion for Yen is {{  }}</li>
        <li id="pounds-result">Your conversion for Pounds is {{  }}</li>
        <li id="zloty-result">Your conversion for Zloty is {{  }}</li>
        <li id="real-result">Your conversion for Real is {{  }}</li>
    </ul>
    <button @click="convertCurrency">test</button>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'NewConverter',
  data () {
    return {
      currencies: [],
      euro: 0,
      result: 0,
      data: {
          categories: []
      }
    }
  },
  mounted() {
    axios.get('http://127.0.0.1:2000/currency')
    .then((response) => {
      this.currencies = response.data;
    }).catch((err) => {
      console.log(err);
    })

  },
  methods: {
      convertCurrency() {
        let checkbox = document.getElementById('dollar', 'yen', 'pounds');
        let text = document.getElementById('dollar-result', 'yen-result', 'pounds-result', 'zloty-result', 'real-result');
        if (checkbox.checked === true) {
            text.style.display = "block";
        } else {
            text.style.display = "none";
        }

      }
  },
  computed: {
    dollarValue() {
        let checkedValue = document.querySelector('input[name="current-currency"]:checked');
        if (checkedValue.value === 'dollar') {
            let value = 0;
            value = this.euro * 1.11;
            return this.result = `$${value.toFixed(2)}`;
        }
    },
    yenValue() {
        let checkedValue = document.querySelector('input[name="current-currency"]:checked');
        if (checkedValue.value === 'yen') {
            let value = this.euro * 122;
            return this.result = `$${value.toFixed(2)}`;
        }
    },
    poundsValue() {
        let checkedValue = document.querySelector('input[name="current-currency"]:checked');
        if (checkedValue.value === 'pounds') {
            let value = this.euro * 0.85;
            return this.result = `$${value.toFixed(2)}`;
        }
    },
    zlotyValue() {
        let checkedValue = document.querySelector('input[name="current-currency"]:checked');
        if (checkedValue.value === 'zloty') {
            let value = this.euro * 4.25;
            return this.result = `$${value.toFixed(2)}`;
        }
    },
    realValue() {
        let checkedValue = document.querySelector('input[name="current-currency"]:checked');
        if (checkedValue.value === 'real') {
            let value = this.euro * 4.52;
            return this.result = `$${value.toFixed(2)}`;
        }
    },
  }
}
</script>


<style>
.row {
    display: flex;
}
#checkboxes input{
    display: inline-block;
    margin-right: 10px;
}
#checkboxes label {
    display: inline-block;
}
#dollar-result, #yen-result, #pounds-result, #zloty-result, #real-result {
    display: none;
}
</style>
