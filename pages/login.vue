<template>
    <div class="login-container">
      <h2 class="login-title">Login</h2>
      <div class="login-field-container">
        <label for="email">Email</label>
        <input id="email" v-model="login.email" type="text" />
        <p v-if="$v.login.email.$dirty && $v.login.email.$invalid && !$v.login.email.email" class="error-message">Enter valid email</p>
        <p v-if="$v.login.email.$dirty && $v.login.email.$invalid && !$v.login.email.required" class="error-message">This field is required</p>
      </div>
      <div class="login-field-container">
        <label for="password">Password</label>
        <input id="password" v-model="login.password" type="password" />
        <p v-if="$v.login.password.$dirty && $v.login.password.$invalid" class="error-message">This field is required</p>
        <p v-if="errors" class="error-message">{{errors}}</p>
      </div>
      <button class="black-btn" @click="loginToAccount">Login</button>
    </div>
  </template>


<script>
import { required, email } from 'vuelidate/lib/validators'
export default {
  data() {
    return {
      login: {
        email: '',
        password: '',
      },
      errors: null
    }
  },
  validations: {
    login: {
        email: {required,email},
        password: {required},
    },
  },
  methods:{
    async loginToAccount(){
        this.$auth.login()
        console.log(this.$auth)
        this.$v.$touch()
        if(!this.$v.$invalid){
            try {
                await this.$axios.post('auth/login',this.login).then(
                    this.$router.push('/')
                )
            } catch (e) {
                this.errors = e.response.data.first_errors.email
            } 
        }
    }
  }
}
</script>
<style lang="scss">
.login-container {
  position: absolute;
  top: 40%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 400px;
  .login-title {
    font-size: 22px;
    font-weight: 600;
    margin-bottom: 20px;
  }
  .login-field-container {
    display: flex;
    flex-direction: column;
    margin-bottom: 15px;

    input {
      height: 35px;
      padding-left: 5px;
      border: 1px solid #d1d1d1;
      outline: none;
      border-radius: 3px;
    }

    label {
      color: rgb(63, 63, 63);
      margin-bottom: 5px;
      font-size: 14px;
      font-weight: 700;
    }
  }
  .black-btn {
    height: 35px;
    background-color: black;
    color: white;
    padding: 0 20px;
    width: 100%;
    outline: 0;
    border: 0;
    border-radius: 3px;
    cursor: pointer;
    font-weight: 500;
  }
  .error-message{
    color: rgb(179, 23, 23);
    padding: 5px 0 0 0;
    font-size: 14px;
  }
  .login{
    display: flex;
    justify-content: center;
    margin-top: 10px;
    color: rgb(63, 63, 63);
    a{
        color: rgb(63, 63, 63);
        text-decoration: none;
    }
  }
}
</style>