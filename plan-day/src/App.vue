<template>
  <div class="container">
    <PlanForm />
  </div>
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
@import "../node_modules/bootstrap/dist/css/bootstrap.css";
</style>
