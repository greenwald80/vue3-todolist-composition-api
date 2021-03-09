<template>
  <div class="task-input my-list">
    <input type="text" placeholder="title" v-model="title" />
    <input type="text" placeholder="description" v-model="description" />
    <button @click="onAddTask">Add task</button>
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  emits: {
    // validation
    onAddTask({ title, description }) {
      if (title === "" || description === "") {
        alert("Fill all fields");
        return false;
      }
      return true;
    },
  },
  //// ref заменяет все это
  // data(){
  //     return{
  //         title: "",description: "",
  //     }
  // },
  setup(props, { emit }) {
    const title = ref("");
    const description = ref("");
    const onAddTask = () => {
      emit("onAddTask", { title: title.value, description: description.value });
    };
    return {
      title,
      description,
      onAddTask,
    };
  },
};
</script>

<style scoped>
.task-input {
  margin: 10px 0;
}
</style>
