<template>
  <h1>Crypto</h1>
  <Input :changeAmount="changeAmount" :convert="convert"/>
  <p v-if="error != ''">{{ error }}</p>
  <p v-if="result != 0">{{ result }}</p>
  <div className="selectors">
    <Selector :setCrypto="setCryptoFirst"/>
    <Selector :setCrypto="setCryptoSecond"/>
  </div>


</template>

<script>
  import Input from './components/Input.vue';
  import Selector from './components/Selector.vue';
  import CryptoConvert from 'crypto-convert';

  const convert = new CryptoConvert();

  export default {
    components: {
      Input,
      Selector
    },
    data() {
      return {
        amount: 0,
        cryptoFirst: '',
        cryptoSecond: '',
        error: '',
        result: 0
      }
    },
    methods: {
      changeAmount(val) {
        this.amount = val
      },
      setCryptoFirst(val) {
        this.cryptoFirst = val
      },
      setCryptoSecond(val) {
        this.cryptoSecond = val
      },
      async convert() {
          if(this.amount == 0) {
            this.error = 'Введите число больше за ноль'
            return;
          }else if(this.cryptoFirst == '' || this.cryptoSecond == '') {
            this.error = 'Выберите валюту'
            return;
          }else if(this.cryptoFirst == this.cryptoSecond) {
            this.error = 'Нельзя конвертировать одинаковые валюты'
            return;
          }

          this.error = '';
          await convert.ready();
          
          this.result = convert.USD.USD(1);
      }
    }
  }
</script>

<style scoped>
.selectors {
  display: flex;
  justify-content: space-around;
  width: 700px;
  margin: 0 auto;
}
</style>
