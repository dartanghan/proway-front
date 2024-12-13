<template>
  Bem vindo ao sistema de alunos Proway
  <form @submit.prevent="handleSubmit">
    <div>
      <label for="username">Username:</label>
      <input type="text" id="username" v-model="username" required>
    </div>
    <div>
      <label for="password">Password:</label>
      <input type="password" id="password" v-model="password" required>
    </div>
    <button type="submit">Submit</button>
  </form>

</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    
  },
  data() {
    return {
      username: '',
      password: ''
    };
  },
  methods: {
    handleSubmit() {
      fetch('http://'+window.location.hostname+':8080/api-auth/login/', {
        method: 'POST',        
        headers: {
          'Content-Type': 'application/json',
          'Origin': 'http://localhost:8081'
        },
        body: JSON.stringify({
          username: this.username,
          password: this.password
        })
      })
      .then(response => {
        console.log(response.status)
        if( response.status == '403' ){
          alert('Comunicacao funcional')
        }
      });
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
