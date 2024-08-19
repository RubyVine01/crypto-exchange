<template>
  <div className="app">
    <h1>Crypto</h1>
    <Input :changeAmount="changeAmount" :convert="convert" :favourite="favourite" />
    <p v-if="error != ''" className="text-error">{{ error }}</p>
    <p v-if="result != ''" className="result-text">{{ result }}</p>
    <div className="selectors">
      <Selector :setCrypto="setConvertFrom" :convertNow="convertFrom" />
      <Selector :setCrypto="setConvertTo" :convertNow="convertTo" />
    </div>
    <Favourite :favs="favs" v-if="favs.length > 0" :getFromFavs="getFromFavs" />
  </div>
</template>

<script>
import Input from './components/Input.vue';
import Selector from './components/Selector.vue';
import Favourite from './components/Favourite.vue';
import CryptoConvert from 'crypto-convert';

const convert = new CryptoConvert();


export default {
  components: { Input, Selector, Favourite },
  data() {
    return {
      amount: 0,
      convertFrom: '',
      convertTo: '',
      error: '',
      result: 0,
      favs: []
    }
  },
  methods: {
    favourite() {

      if (this.favs.length >= 3) {
        this.error = 'Максимальное количество в избранном 3';
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
      this.favs.push({
        from: this.convertFrom,
        to: this.convertTo
      })
    },
    getFromFavs(index) {
      this.convertFrom = this.favs[index].from;
      this.convertTo = this.favs[index].to
    },
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
    },

  }
}
</script>

<style scoped>
.app {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.selectors {
  display: flex;
  justify-content: space-between;
  width: 570px;
  margin: 20px  0;
}

.text-error {
  color: rgb(211, 1, 176);
  margin: 10px;
}
</style>
