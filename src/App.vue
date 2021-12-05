<!-- App.vue -->

<template>
  <div id="app">
    <TodoHeader />
    <TodoList
      :data="data"
      v-on:modalOpen="handleOpen"
      v-on:modalUpdate="handleUpdate"
    />
    <TodoInput
      v-if="openModal === true"
      v-on:handleClose="handleClose"
      v-on:handleConfirm="handleConfirm"
      v-on:handleDelete="handleDelete"
      :id="id"
      :from="from"
      :to="to"
      :title="title"
      :bgColor="bgColor"
      :status="status"
    />
  </div>
</template>

<script>
import TodoHeader from "./components/TodoHeader";
import TodoList from "./components/TodoList";
import TodoInput from "./components/TodoInput";

export default {
  name: "App",
  components: {
    TodoHeader,
    TodoList,
    TodoInput,
  },
  data() {
    return {
      data: [],
      openModal: false,
      id: 0,
      from: "",
      to: "",
      title: "",
      bgColor: "",
      status: "",
      lastId: 0,
    };
  },
  methods: {
    handleOpen({ bgColor, status }) {
      this.id = this.lastId + 1;
      this.from = "";
      this.to = "";
      this.title = "";
      this.bgColor = bgColor;
      this.status = status;
      this.openModal = true;
    },
    handleClose() {
      this.openModal = false;
    },
    handleUpdate({ id, from, to, title, bgColor, status }) {
      this.id = id;
      this.from = from;
      this.to = to;
      this.title = title;
      this.bgColor = bgColor;
      this.status = status;
      this.openModal = true;
    },
    handleConfirm({ id, from, to, title, bgColor, status }) {
      this.openModal = false;
      const newData = [
        ...this.data.filter((el) => el.id !== id),
        { id, from, to, title, bgColor, status },
      ].sort(function (a, b) {
        return a.id - b.id;
      });
      this.lastId = newData[newData.length - 1].id;
      this.data = newData;
      localStorage.setItem("todo", JSON.stringify(newData));
    },
    handleDelete(id) {
      this.openModal = false;
      const newData = [...this.data.filter((el) => el.id !== id)];
      this.data = newData;
      localStorage.setItem("todo", JSON.stringify(newData));
    },
  },
  created() {
    const todoData = JSON.parse(localStorage.getItem("todo"));
    this.data = todoData;
    this.lastId = todoData[todoData.length - 1].id;
  },
};
</script>

<style lang="scss">
@import "./assets/style/reset.scss";
body {
  width: 100%;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #333;
  color: whitesmoke;
  position: relative;
}
#app {
  width: 80%;
  height: 100vh;
  box-sizing: border-box;
  padding: 1rem;
}
</style>
