<template>
  <h1>Crypto</h1>
  <Input :changeAmount="changeAmount" />
  <div className="selectors">
    <Selector :setCrypto="setConvertFrom" />
    <Selector :setCrypto="setConvertTo" />
  </div>


</template>

<script>
import Input from './components/Input.vue';
import Selector from './components/Selector.vue'
export default {
  components: { Input, Selector },
  data() {
    return {
      amount: 0,
      convertFrom: '',
      convertTo: ''
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
