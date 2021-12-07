<template>
  <img alt="Vue logo" src="./assets/logo.png" />
  <PlanForm />
</template>

<script lang="ts">
import { Options, Vue } from "vue-class-component";
import PlanForm from "./components/PlanForm.vue";

@Options({
  components: {
    PlanForm,
  },
})
export default class App extends Vue {}
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
