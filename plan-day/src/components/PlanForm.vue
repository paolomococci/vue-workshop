<template>
  <div class="mb-4">
    <h1>Plan From at work!</h1>
    <hr />
    <h3>TypeScript demo {{ version }}</h3>
  </div>
  <form @submit.prevent="addNewTask">
    <div class="mb-5">
      <label for="newTask" class="form-label"> New Task </label>
      <input
        class="form-control"
        id="newTask"
        placeholder="task to be scheduled"
        v-model="newTask"
        name="newTask"
      />
      <div class="m-2">
        <button type="submit" class="btn btn-primary">add new task</button>
      </div>
    </div>
  </form>
  <div v-if="tasks.length === 0">
    <h4>the list of tasks to be performed is empty</h4>
  </div>
  <div v-else>
    <ul class="list-group">
      <li class="list-group-item" v-for="task in tasks" :key="task.id">
        <h4>{{ task.content }}</h4>
      </li>
    </ul>
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
    const tasks = ref<PlanType[]>([]);

    function addNewTask(): void {
      if (!newTask.value) {
        return;
      }
      tasks.value.push({
        id: uuidv4(),
        done: false,
        content: newTask.value,
      });
      console.log("new task: ", newTask.value);
      newTask.value = "";
    }

    return {
      version,
      tasks,
      newTask,
      addNewTask,
    };
  },
});
</script>
