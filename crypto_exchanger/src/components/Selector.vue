<template>
    <ul>
        <li @click="selectItem('BTC')" :class="{ active: current === 'BTC'}">Bitcoin</li>
        <li @click="selectItem('ETH')" :class="{ active: current === 'ETH'}">ETH</li>
        <li @click="selectItem('USDT')" :class="{ active: current === 'USDT'}">USDT</li>
        <li @click="selectItem('TON')" :class="{ active: current === 'TON'}">TON</li>
        <li @click="selectItem('NOT')" :class="{ active: current === 'NOT'}">NOT</li>
    </ul>
</template>
  
<script>
export default {
   props: {
    setCrypto: {
        type: Function,
        required: true
    },
   },
   data() {
        return {
            current: ''
        }
    },
    methods: {
        selectItem(val) {
            this.setCrypto(val);
            this.current = val;
        }
    }
   
}
</script>
  
<style scoped>
ul{
    list-style: none;
    width: 200px;
    padding: 0;
    border-radius: 3px;
    border: 3px solid black;
}

li {
    display: block;
    background: #1A032D;
    color: white;
    padding: 20px 0;
}

li:hover, li.active{
    background: #0e0118;
    cursor: pointer;
}

</style>
  