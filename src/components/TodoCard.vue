<template>
  <div class="card" @click="updateModal">
    <div class="date">
      <span>
        <p>{{ this.from + " ~ " + this.to }}</p>
      </span>
    </div>
    <p class="title">{{ this.title }}</p>
  </div>
</template>

<script>
export default {
  props: {
    id: Number,
    from: String,
    to: String,
    title: String,
    status: String,
  },
  data() {
    return {
      bgColor: "",
    };
  },
  methods: {
    getColor() {
      const palette = {
        "No Status": "slategrey",
        "Next Up": "goldenrod",
        "In Progress": "darkgreen",
        Completed: "darkmagenta",
      };
      this.bgColor = palette[this.status];
    },
    updateModal() {
      this.$emit("modalUpdate", {
        id: this.id,
        from: this.from,
        to: this.to,
        title: this.title,
        bgColor: this.bgColor,
        status: this.status,
      });
    },
  },
  created() {
    this.getColor();
  },
};
</script>

<style lang="scss" scoped>
.card {
  background-color: rgb(67, 71, 75);
  border: 1px solid rgba(37, 40, 43, 0.7);
  border-radius: 8px;
  margin-bottom: 0.3rem;
  min-height: 100px;
  width: 100%;
  & .date {
    display: flex;
    padding: 0.5rem;
    & span {
      background: rgba(37, 40, 43, 0.7);
      border-radius: 4px;
      display: block;
      height: max-content;
      padding: 4px 8px;
      width: max-content;
      & p {
        font-size: 0.8rem;
      }
    }
  }
  & .title {
    font-size: 0.8rem;
    padding: 0 0.8rem 0.8rem;
  }
}
</style>
