<template>
  <div>

    <form action="">
      <input type="text" v-model="nome">

      <vue-recaptcha
              ref="recaptcha"
              @verify="onVerify"
              @expired="onExpired"
              :sitekey="sitekey">
      </vue-recaptcha>
      <!--<button @click="resetRecaptcha"> Reset ReCAPTCHA</button>-->
      <button type="button" @click="postar()"> Enviar </button>

    </form>
  </div>
</template>

<script>

  import VueRecaptcha from 'vue-recaptcha';


  export default {
    name: 'HelloWorld',
    components: {VueRecaptcha},
    data() {
      return {
        msg: 'Welcome to Your Vue.js App',
        nome :'',
        captcha:false,
        sitekey: ''
      }
    },
    methods: {
      postar(){
        if(!this.captcha){
          alert("marcar captchar");
          return false;
        }
        console.log('postar');
        return false;
      },
      onSubmit: function () {
        this.$refs.recaptcha.execute()
      },
      onVerify: function (response) {
        this.captcha = response;
        console.log('Verify: ' + response)
      },
      onExpired: function () {
        console.log('Expired')
      },
      resetRecaptcha() {
        this.$refs.recaptcha.reset() // Direct call reset method
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  h1, h2 {
    font-weight: normal;
  }

  ul {
    list-style-type: none;
    padding: 0;
  }

  li {
    display: inline-block;
    margin: 0 10px;
  }

  a {
    color: #42b983;
  }
</style>
