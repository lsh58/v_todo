<!-- App.vue -->

<template>
  <div id="app">
    <TodoHeader />
    <TodoInput />
    <TodoList />
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
}
#app {
  width: 80%;
  height: 100vh;
  box-sizing: border-box;
  padding: 1rem;
}
</style>
