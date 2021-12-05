<template>
  <header>
    <h1 class="title">{{ title }}</h1>
    <h2 class="date">{{ timestamp }}</h2>
  </header>
</template>

<script>
export default {
  data() {
    return {
      title: "📅 To-Do",
      timestamp: "",
    };
  },
  created() {
    const now = new Date();
    const year = now.getFullYear();
    const month = now.getMonth() + 1;
    const date = now.getDate();
    const weekList = new Array("SUN", "MON", "TUE", "WED", "THU", "FRI", "SAT");
    const week = weekList[now.getDay()];
    this.timestamp = `${year}.${month}.${
      date > 9 ? date : "0" + date
    }. ${week}`;
  },
};
</script>

<style lang="scss" scoped>
header {
  align-items: baseline;
  display: flex;
  justify-content: space-between;
  padding-bottom: 16px;
  padding-top: 16px;
}
.title {
  font-size: 2rem;
  font-weight: 600;
}
.date {
  font-size: 2rem;
  font-weight: 100;
}
</style>
