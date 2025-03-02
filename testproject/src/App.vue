<template>
  <input type="text" v-model="userName" placeholder="Имя">
  <input type="password" v-model="userPassword"  placeholder="Пароль">
  <input type="email" v-model="userEmail"  placeholder="Почта">
  <p className="error">{{ error }}</p>
  <button @click="sendData()">Отправить</button>

  <div v-if="users.length == 0" className = "user" >
    Пользователей не найдено
  </div>
  <User v-for="(el, index) in users" :key="index" :user="el" :index="index" :deleteUser="deleteUser"/>
</template>

<script>

import User from './components/User.vue'
  export default {
    components: {
      User
    },
    data() {
      return {
        users: [],
        error: '',
        userName: '',
        userPassword: '',
        userEmail: ''
      }
    },
    methods: {
      insertData(val) {
        this.userName = val
      },
      sendData() {
        if(this.userName == '') {
          return this.error = "Имя не введено";
        }
        else if (this.userEmail == '') {
          return this.error = "Email не введен";
        }
        else if (this.userPassword == '') {
          return this.error = "Пароль не введен";
        }

        this.error = '';
        this.users.push({
          name: this.userName,
          pass: this.userPassword,
          email: this.userEmail,
        })
        this.clearForms()
        
      },
      deleteUser(index) {
        this.users.splice(index,1);
      },
      clearForms() {
        this.userName = '',
        this.userPassword = '',
        this.userEmail = ''
      }
    }
  }

</script>

<style scoped>

input {
  display: block;
  margin-bottom: 10px;
  border-radius: 3px;
  border: 1px solid silver;
  outline: none;
  padding: 10px 15p;
  background: #fafafa;
  color: #333;
}

button {
  border: 0;
  border-radius: 5px;
  outline: none;
  padding: 10px 15px;
  margin-bottom: 10px;
  background: #6cd670;
  color: #167f3d;
  font-weight: bold;
  cursor: pointer;
  transition: transform 500ms ease;
}

button:hover {
  transform: translateY(-5px);
}

.user {
  width: 500px;
  margin-bottom: 20px;
  border: 1px solid silver;
  background: #e3e3e3;
  color: #000;
  padding: 20px;
  border-radius: 5px;
}

</style>
