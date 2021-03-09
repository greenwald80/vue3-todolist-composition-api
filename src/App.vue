<template>
  <main>
    <TaskInput @onAddTask="addTask"></TaskInput>
    <hr />
    <ul class="task-list my-list">
      <li v-for="item in taskList" :key="item.id">
        <TaskCard
          :model="item"
          @onRemove="removeTask(item.id)"
          @onDone="setDoneTask(item.id)"
        ></TaskCard>
      </li>
    </ul>
  </main>
</template>

<script>
import TaskCard from "./components/TaskCard.vue";
import TaskInput from "./components/TaskInput.vue";
import { ref } from "vue";

export default {
  name: "App",
  components: {
    TaskCard,
    TaskInput,
  },
  setup() {
    const taskList = ref([
      { id: 0, title: "title", description: "description", status: false },
    ]);

    const addTask = ({ title, description }) => {
      taskList.value = [
        ...taskList.value,
        {
          id: taskList.value[taskList.value.length - 1].id + 1,
          title,
          description,
          status: false,
        },
      ];
    };

    const setDoneTask = (id) => {
      taskList.value = taskList.value.map((x) => {
        if (x.id === id) x.status = true;
        return x;
      });
    };

    const removeTask = (id) => {
      taskList.value = taskList.value.filter((x) => x.id !== id);
    };

    return {
      taskList,
      addTask,
      setDoneTask,
      removeTask,
    };
  },
};
</script>

<style scoped>
.task-list {
  list-style: none;
}
</style>
