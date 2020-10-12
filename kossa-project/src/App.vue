<template>
  <v-app>
    <router-view />
  </v-app>
</template>

<script>
//import HomeView from "./views/Home";

export default {
  name: "App",

  components: {
    //HomeView,
  },
  mounted() {
    console.log(this.$firebase);
  },
  data: () => ({
    //
  }),
  methods: {}
};
</script>
<style scoped>
button {
  height: 500px;
}
</style>
