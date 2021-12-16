<template>
  <div class="home fill-height d-flex justify-center align-center">
    <HelloWorld msg="Welcome to Globetrotter web application" />
  </div>
</template>

<script lang="ts">
import { Options, Vue } from "vue-class-component";
import HelloWorld from "@/components/HelloWorld.vue";

@Options({
  components: {
    HelloWorld,
  },
})
export default class Home extends Vue {}
</script>
