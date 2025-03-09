<script>
import { computed } from 'vue';
import axios from 'axios';



export default {
  data() {
    return {
      city: "",
      error: "",
      info: null
    }
  },
  computed: {
    cityName() {
      return "«" +this.city + "»"
    }
  },
  methods: {
    getApiData() {
      if(this.city.trim().length <= 2) {
        this.error = "Название слишком короткое";
        return false;
      }
      
      axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=ab65444dec29e2bd823475284b602c42`)
      .then(res => (this.info = res.data))

      console.log(this.info)
    }
  }
}

</script>

<template>
  <div class="wrapper">
    <h1>Погодное приложение</h1>
    <p>Узнать погоду в {{ city == "" ? "вашем городе" :  cityName}}</p>
    <input type="text" v-model="city" placeholder="Введите город">
    <button v-show="city.length > 0 " @click="getApiData()" >Получить погоду</button>
    <p class="error" v-if="getApiData() == false" >{{ error }}</p>
    <p v-if="info != null">{{ info.main.temp }}</p>
  </div>
</template>

<style scoped>

.error {
  color: red;

}

.wrapper {
  width: 900px;
  height: 500px;
  border-radius: 50px;
  background: #1f0f24;
  padding: 20px;
  color: #fff;
  text-align: center;
}

.wrapper h1 {
  margin-top: 50px;
}

.wrapper p{
  margin-top: 20px;
}

.wrapper input {
  margin-top: 30px;
  background: transparent;
  border: 0;
  border-bottom: 2px solid #110813;
  color: #fcfcfc;
  font-size: 14px;
  padding: 5px 8px;
  outline: none;

}

.wrapper input:focus {
  border-bottom-color: #6e2d7d;
}

.wrapper button {
  background: #e3bc4b;
  color: #fff;
  border-radius: 10px;
  border: 2px solid #b99935;
  padding: 10px 15px;
  margin-left: 20px;
  cursor: pointer;
  transition: transform 500ms ease;

}
.wrapper button:hover {
  transform: scale(1.1) translateY(-5px);
}

</style>
