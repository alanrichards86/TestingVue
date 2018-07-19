<template>
  <div class="home">
    <img src="../../assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  
    <div id="formDivId">
      <form id="homeForm" @submit.prevent="onSubmit">
        
        <p class="errMsgs" v-if="errors.length">
          Please fix the following errors(s):
          <ul>
            <li class="err" v-for="(error, index) in errors" :key="index">{{ error }}</li>
          </ul>
        </p>

        <input type="text" name="name" id="name" v-model="name" placeholder="name">

        <input type="email" name="email" v-model="email" placeholder="email">

      <button type="submit">Submit info</button>
      </form>
    </div>

    <div>
      <p>This is your name: {{name}}</p>
      <p>This is your email address: {{email}}</p>
    </div>
    <LoggedIn id="loggedInComponent" v-show="loggedIn" />
  </div>
</template>

<script>

// @ is an alias to /src
import HelloWorld from '@/components/home/HelloWorld.vue'
import LoggedIn from './LoggedIn.vue'

export default {
  name: 'home',
  components: {
    HelloWorld,
    LoggedIn
  },
  data () {
    return {
      errors: [],
      name: '',
      email: '',
      loggedIn: false
    }
  },
  methods: {
    onSubmit(e) {
      this.errors = [];
      console.log(e);
      if(this.name && this.email) {
        this.name = '';
        this.email = '';
        this.loggedIn = true;
        return true;
      }else if(!this.name && this.email) {
        this.errors.push('Name is required.');
      }else if(!this.email && this.name) {
        this.errors.push('Email is requried');
      }
      
    }

  }
}
</script>

<style scoped lang="scss">
  
  #formDivId {
    display: flex;
    justify-content: center;
    width: 100%;
    align-content: center;
  }

  #homeForm {
    width: 30%;
    display: flex;
    flex-direction: column;
  }

  .err {
    list-style: none;
    text-decoration: underline;
    color: red;
  }

  button {
    width: 20%;
    margin-left: 40%;
  }

  input {
    padding: 10px;
    margin: 10px;
  }

  #loggedInComponent {
    margin: 10%;
  }

</style>

