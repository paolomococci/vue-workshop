<template>
  <div class="card" style="margin-top: 20px">
    <div class="card-body">
      <h2 class="card-title">Plan From at work!</h2>
      <h3 class="card-subtitle mb-2 text-muted">
        sample of web application {{ version }}
      </h3>
      <div>
        <form @submit.prevent="addNewTask">
          <div class="mb-5">
            <label for="newTask" class="form-label">
              Type a name for add new task:
            </label>
            <input
              class="form-control"
              id="newTask"
              placeholder="task to be scheduled"
              v-model="newTask"
              name="newTask"
            />
            <div class="d-grid gap-2 d-md-flex justify-content-md-end">
              <div class="m-2">
                <button type="submit" class="btn btn-outline-primary btn-lg">
                  add a new task
                </button>
              </div>
              <div class="m-2">
                <button
                  type="button"
                  class="btn btn-outline-danger btn-lg"
                  @click="removeAllTask"
                >
                  remove all task
                </button>
              </div>
              <div class="m-2">
                <button
                  type="button"
                  class="btn btn-outline-success btn-lg"
                  @click="allCheckAsDone"
                >
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
              <div v-if="task.done">
                <button
                  type="button"
                  class="btn btn-outline-warning btn-sm"
                  @click="removeTask(index)"
                >
                  remove task
                </button>
              </div>
              <div v-else>
                <button
                  type="button"
                  class="btn btn-outline-warning btn-sm"
                  disabled
                  @click="removeTask(index)"
                >
                  remove task
                </button>
              </div>
            </li>
          </ul>
        </div>
      </div>
    </div>
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
  text-decoration: whitesmoke line-through;
}
</style>
