<template>
  <v-main class="grey lighten-3">
    <div class="login">
      <img class="logo" src="../assets/logo.png" /><br />
      <div class="idBox">
        <v-icon>mdi-email</v-icon>
        <input
          class="idInput"
          type="text"
          placeholder="Email"
          v-model="email"
        />
      </div>
      <div class="pwBox">
        <v-icon>mdi-lock</v-icon>
        <input
          class="pwInput"
          type="password"
          placeholder="Password"
          v-model="password"
        />
      </div>
      <v-btn color="#4ebd80" elevation="2" class="loginBtn" @click="login">
        로그인
      </v-btn>
      <br />
      <router-link class="toSignup" to="/signup"
        >계정이 없으신가요?</router-link
      >
    </div>
  </v-main>
</template>

<script>
export default {
  name: "login",
  data() {
    return {
      email: "",
      password: ""
    };
  },
  methods: {
    login() {
      this.$firebase
        .auth()
        .signInWithEmailAndPassword(this.email, this.password)
        .then(
          () => {
            alert("로그인 성공!");
            this.$router.replace("/");
          },
          function(error) {
            alert(`ERROR : ${error.message}`);
          }
        );
    }
  }
};
</script>

<style scoped>
* {
  text-align: center;
  font-family: "Varela Round", sans-serif;
}
input {
  outline: none;
  text-align: left;
  color: rgb(55, 55, 55);
}
.login {
  position: absolute;
  top: 0;
  bottom: 0;
  right: 0;
  left: 0;
  margin: auto;
  width: 400px;
  height: 450px;
  background: white;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.15);
}
.logo {
  width: 300px;
  height: 100px;
  margin-top: 50px;
  margin-bottom: 20px;
}
.idBox,
.pwBox {
  border: 1px solid #dad4d4;
  width: 70%;
  height: 50px;
  margin: 0 auto;
  line-height: 50px;
  margin-bottom: 10px;
  padding-left: 10px;
}
.idInput,
.pwInput {
  width: 80%;
  margin-left: 15px;
  font-size: 13px;
}
.loginBtn {
  margin-top: 15px;
  margin-bottom: 15px;
  width: 65%;
  color: white;
  font-weight: bold;
}
.toSignup {
  color: grey;
  text-decoration: none;
  font-size: 11px;
}
</style>
