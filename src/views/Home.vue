<template>
  <div class="home">
    <form v-on:submit.prevent="login">
      <input type="text" placeholder="email" v-model="email" />
      <input type="password" placeholder="password" v-model="password" />
      <button type="submit">Login</button>
    </form>
  </div>
</template>

<script>
export default {
  name: 'Home',
  data() {
    return {
      email: '',
      password: '',
    };
  },
  methods: {
    login() {
      fetch('http://localhost:3030/auth/login', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify({
          email: this.email,
          password: this.password,
        }),
      })
        .then((res) => res.json())
        .then((data) => {
          console.log(data);
          if (data.token) {
            localStorage.setItem('token', data.token);
          }
        });
    },
  },
};
</script>
