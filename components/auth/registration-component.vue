<template>
  <div class="registration-container">
    <h2 class="registration-title">Registration</h2>
    <div class="registration-field-container">
      <label for="name">Name</label>
      <input id="name" v-model="registration.name" type="text" />
      <p v-if="$v.registration.name.$dirty && $v.registration.name.$invalid" class="error-message">This field is required</p>
    </div>
    <div class="registration-field-container">
      <label for="email">Email</label>
      <input id="email" v-model="registration.email" type="text" />
      <p v-if="errors" class="error-message">{{errors}}</p>
      <p v-if="$v.registration.email.$dirty && $v.registration.email.$invalid && !$v.registration.email.email" class="error-message">Enter valid email</p>
      <p v-if="$v.registration.email.$dirty && $v.registration.email.$invalid && !$v.registration.email.required" class="error-message">This field is required</p>
    </div>
    <div class="registration-field-container">
      <label for="password">Password</label>
      <input id="password" v-model="registration.password" type="password" />
      <p v-if="$v.registration.password.$dirty && $v.registration.password.$invalid" class="error-message">This field is required</p>
    </div>
    <button class="black-btn" @click="submit">Submit</button>
    <div class="login">Already got an account? <nuxt-link to="/login"> Login</nuxt-link></div>
  </div>
</template>


<script>
import { required, email } from 'vuelidate/lib/validators'
export default {
  data() {
    return {
      registration: {
        name: '',
        email: '',
        password: '',
      },
      errors: null
    }
  },
  validations: {
    registration: {
        name: {required},
        email: {required,email},
        password: {required},
    },
  },
  methods:{
    async submit(){
        this.$v.$touch()
        if(!this.$v.$invalid){
            try {
                await this.$axios.post('auth/signup',this.registration).then(
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
.registration-container {
  position: absolute;
  top: 40%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 400px;
  .registration-title {
    font-size: 22px;
    font-weight: 600;
    margin-bottom: 20px;
  }
  .registration-field-container {
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