<template>
  <div class="list">
    <div class="stateWrapper" v-for="(state, i) in states" :key="i">
      <span :style="state.style">
        <h3>{{ state.title }}</h3>
      </span>
      <ul>
        <li v-for="(todo, i) in state.todos" :key="i">
          <TodoCard
            :id="todo.id"
            :from="todo.from"
            :to="todo.to"
            :title="todo.title"
            :status="todo.status"
            v-on:modalUpdate="updateModal"
          />
        </li>
      </ul>
      <button @click="openModal(state)">{{ newCard }}</button>
    </div>
  </div>
</template>

<script>
import TodoCard from "./TodoCard";
export default {
  props: { data: Array },
  data() {
    return {
      newCard: " + 새로만들기 ",
      states: [
        {
          title: "No Status",
          style: { backgroundColor: "slategrey" },
        },
        {
          title: "Next Up",
          style: { backgroundColor: "goldenrod" },
        },
        {
          title: "In Progress",
          style: { backgroundColor: "darkgreen" },
        },
        {
          title: "Completed",
          style: { backgroundColor: "darkmagenta" },
        },
      ],
    };
  },
  components: {
    TodoCard,
  },
  methods: {
    openModal({ title, style }) {
      const status = title;
      const bgColor = style.backgroundColor;
      this.$emit("modalOpen", { bgColor, status });
    },
    updateModal({ id, from, to, title, bgColor, status }) {
      this.$emit("modalUpdate", { id, from, to, title, bgColor, status });
    },
  },
  created() {
    if (this.data?.length > 0) {
      this.states.forEach((state) => {
        state.todos = this.data.filter((el) => el.status === state.title);
      });
    }
  },
};
</script>

<style lang="scss" scoped>
.list {
  border-top: 1px solid rgba(255, 255, 255, 0.2);
  display: flex;
  padding-top: 16px;
  & .stateWrapper {
    box-sizing: border-box;
    min-height: 600px;
    padding: 0 0.5rem;
    width: 25%;
    & span {
      border-radius: 4px;
      display: block;
      height: max-content;
      padding: 0.3rem 0.5rem;
      width: max-content;
      & h3 {
        font-size: 0.8rem;
      }
    }
    & ul {
      padding-bottom: 0.2rem;
      padding-top: 0.5rem;
      & li {
        width: 100%;
      }
    }
    & button {
      background: none;
      border: none;
      color: whitesmoke;
      font-size: 0.8rem;
      cursor: pointer;
    }
  }
}
</style>
