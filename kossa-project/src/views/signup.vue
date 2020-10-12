<template>
  <v-main class="grey lighten-3">
    <div class="login">
      <img class="logo" src="../assets/logo.png" />
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
      <div class="pwBox">
        <v-icon>mdi-lock</v-icon>
        <input
          class="pwInput"
          type="password"
          placeholder="Confirm Password"
          v-model="password2"
        />
      </div>
      <v-btn color="#4ebd80" elevation="2" class="loginBtn" @click="signUp"
        >회원가입</v-btn
      ><br />
      <router-link class="toLogin" to="/login">
        로그인 창으로 돌아가기
      </router-link>
    </div>
  </v-main>
</template>

<script>
export default {
  name: "login",
  data() {
    return {
      email: "",
      password: "",
      password2: ""
    };
  },
  methods: {
    signUp() {
      if (this.password != this.password2) {
        alert("ERROR : Password does not match");
        return;
      }
      this.$firebase
        .auth()
        .createUserWithEmailAndPassword(this.email, this.password)
        .then(
          () => {
            alert("회원가입 완료!");
            this.$router.replace("login");
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
  height: 500px;
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
.toLogin {
  color: grey;
  text-decoration: none;
  font-size: 11px;
}
</style>
