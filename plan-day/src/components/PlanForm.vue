<template>
  <div class="mb-4">
    <h1>Plan From at work!</h1>
    <hr />
    <h3>TypeScript demo {{ version }}</h3>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";
import { PlanType } from "@/models/planModel";
import { v4 as uuidv4 } from "uuid";

export default defineComponent({
  name: "PlanForm",
  setup() {
    const version = ref("version 1.0");
    const newTask = ref("");
    const task = ref<PlanType[]>([]);

    function addNewTask(): void {
      if (!newTask.value) {
        return;
      }
      task.value.push({
        id: uuidv4(),
        done: false,
        content: newTask.value,
      });
      console.log("new task: ", newTask.value);
      newTask.value = "";
    }

    return {
      version,
      task,
      newTask,
      addNewTask
    };
  },
});
</script>
