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
