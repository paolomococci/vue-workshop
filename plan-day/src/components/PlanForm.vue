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
      <div class="mb-5 d-flex flex-row justify-content-start">
        <div class="m-2">
          <button type="submit" class="btn btn-primary">add a new task</button>
        </div>
        <div class="m-2">
          <button type="button" class="btn btn-danger" @click="removeAllTask">
            remove all task
          </button>
        </div>
        <div class="m-2">
          <button type="button" class="btn btn-success" @click="allCheckAsDone">
            all check as done
          </button>
        </div>
      </div>
    </div>
  </form>
  <div v-if="tasks.length === 0">
    <h4>the list of tasks to be performed is empty</h4>
  </div>
  <div v-else>
    <ul class="list-group">
      <li
        class="list-group-item d-flex flex-row justify-content-between align-items-center"
        v-for="(task, index) in tasks"
        :key="task.id"
      >
        <h4
          :class="{ mark: task.done }"
          style="cursor: pointer"
          @click="checkAsDone(task)"
        >
          {{ task.content }}
        </h4>
        <button
          type="button"
          class="btn btn-warning"
          @click="removeTask(index)"
        >
          remove task
        </button>
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
import { defineComponent, onMounted, PropType, ref } from "vue";
import { PlanType } from "@/models/planModel";
import { v4 as uuidv4 } from "uuid";

type Props = {
  title: string;
  subTitle: string;
};

export default defineComponent({
  name: "PlanForm",
  props: {
    about: {
      type: Object as PropType<Props>,
      required: true,
    },
  },
  setup(props) {
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

    function checkAsDone(task: PlanType): void {
      task.done = !task.done;
    }

    function removeTask(index: number): void {
      tasks.value.splice(index, 1);
    }

    function removeAllTask(): void {
      tasks.value = [];
    }

    function allCheckAsDone(): void {
      tasks.value.forEach((task) => (task.done = true));
    }

    onMounted(() => console.log(props.about.title));

    return {
      version,
      tasks,
      newTask,
      addNewTask,
      checkAsDone,
      removeTask,
      removeAllTask,
      allCheckAsDone,
    };
  },
});
</script>

<style>
.mark {
  text-decoration: aquamarine;
}
</style>
