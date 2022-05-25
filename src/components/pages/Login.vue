<template>
  <div>
    <form @submit.prevent="signin" class="form-signin">
    <h1 class="h3 mb-3 fw-normal">請登入</h1>
      <label for="floatingInput" class="sr-only">Email address</label>
      <input type="email" class="form-control" id="floatingInput" placeholder="Email address" v-model="user.username" required>
      <label for="floatingPassword" class="sr-only">Password</label>
      <input type="password" class="form-control" id="floatingPassword" placeholder="Password" v-model="user.password">
    <div class="checkbox mb-3">
      <label>
        <input type="checkbox" value="remember-me"> Remember me
      </label>
    </div>
    <button class="btn btn-lg btn-primary btn-block" type="submit">Sign in</button>
    <p class="mt-5 mb-3 text-muted">&copy; 2017–2022</p>
  </form>
  </div>    
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      user:{
          username:'',
          password:'',
      }
    }
  },
  methods:{
      signin(){
    const api = `${process.env.APIPATH}/signin`;
    const vm = this;
    this.$http.post(api, vm.user).then((response) => {
      console.log(response.data);
      if(response.data.success){
          const token = response.data.token;
          const expired = response.data.expired;
          console.log(token, expired);
      }
  });
      }
  }
}
</script>
<style scoped>
html,
body {
  height: 100%;
}

body {
  display: -ms-flexbox;
  display: flex;
  -ms-flex-align: center;
  align-items: center;
  padding-top: 40px;
  padding-bottom: 40px;
  background-color: #f5f5f5;
}

.form-signin {
  width: 100%;
  max-width: 330px;
  padding: 15px;
  margin: auto;
}
.form-signin .checkbox {
  font-weight: 400;
}
.form-signin .form-control {
  position: relative;
  box-sizing: border-box;
  height: auto;
  padding: 10px;
  font-size: 16px;
}
.form-signin .form-control:focus {
  z-index: 2;
}
.form-signin input[type="email"] {
  margin-bottom: -1px;
  border-bottom-right-radius: 0;
  border-bottom-left-radius: 0;
}
.form-signin input[type="password"] {
  margin-bottom: 10px;
  border-top-left-radius: 0;
  border-top-right-radius: 0;
}
</style>
<!-- Add "scoped" attribute to limit CSS to this component only -->

