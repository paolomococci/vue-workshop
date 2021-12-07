<template>
  <div class="mb-4">
    <h1>Plan From at work!</h1>
    <hr />
    <h3>TypeScript demo {{ version }}</h3>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";
export default defineComponent({
  name: "PlanForm",
  setup() {
    const version = ref("version 1.0");
    return { version };
  },
});
</script>
