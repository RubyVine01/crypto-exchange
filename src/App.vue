<template>
  <h1>Crypto</h1>
  <Input :changeAmount="changeAmount" :convert="convert" />
  <p v-if="error != ''">{{ error }}</p>
  <p v-if="result != ''" className="result-text">{{ result }}</p>
  <div className="selectors">
    <Selector :setCrypto="setConvertFrom" />
    <Selector :setCrypto="setConvertTo" />
  </div>
</template>

<script>
import Input from './components/Input.vue';
import Selector from './components/Selector.vue';
import CryptoConvert from 'crypto-convert';

const convert = new CryptoConvert();


export default {
  components: { Input, Selector },
  data() {
    return {
      amount: 0,
      convertFrom: '',
      convertTo: '',
      error: '',
      result: 0,
    }
  },
  methods: {
    changeAmount(val) {
      this.amount = val
    },
    setConvertFrom(val) {
      this.convertFrom = val
    },
    setConvertTo(val) {
      this.convertTo = val
    },
    async convert() {
      if (this.amount <= 0) {
        this.error = 'Пожалуйста, укажите число больше нуля.';
        return
      }
      else if (this.convertFrom == '' || this.convertTo == '') {
        this.error = 'Выберите валюту.';
        return
      }
      else if (this.convertFrom == this.convertTo) {
        this.error = 'Выберите другую валюту.';
        return
      }

      this.error = ""
      await convert.ready();
      this.result = convert[this.convertFrom][this.convertTo](this.amount);
    }

  }
}
</script>


<style scoped>
.selectors {
  display: flex;
  justify-content: space-around;
  width: 700px;
  margin: 20px auto;
}
</style>
