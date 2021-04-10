<template>
  <!-- <img alt="Vue logo" src="./assets/logo.png" /> -->
  <HelloWorld msg="Hello Vue 3 + TypeScript + Vite" />
  <Icon :icon="xa" :size="24" />
  <Icon :icon="xa" :size="24" />
  <Icon :icon="'uil:heart-sign'" :size="24" />
  <Icon :icon="'ant-design:customer-service-filled'" :size="24" />

 
</template>

<script lang="ts">
import { defineComponent } from "vue";
import HelloWorld from "./components/HelloWorld.vue";
import Icon from "./components/Icon/Icon.vue";
export default defineComponent({
  name: "App",
  components: {
    HelloWorld,
    Icon,
  },
  data(){
    return{
      xa :'mdi-light:folder'
    }
  }
});
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