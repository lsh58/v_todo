<template>
  <div class="input">
    <div class="modal">
      <div class="modalHeader">
        <span :style="this.style">
          <h3>{{ this.status }}</h3>
        </span>
      </div>
      <div class="date">
        <p>Date From</p>
        <input class="date" type="date" v-model="dateFrom" />
      </div>
      <div class="date">
        <p>Date To</p>
        <input class="date" type="date" v-model="dateTo" />
      </div>
      <input class="title" type="text" v-model="modalTitle" />
      <div class="btnWrapper">
        <button class="deleteBtn" @click="deleteModal">Delete</button>
        <div class="rightBtn">
          <button class="closeBtn" @click="closeModal">Close</button>
          <button class="confirmBtn" @click="confirmModal">Confirm</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    id: Number,
    from: String,
    to: String,
    title: String,
    bgColor: String,
    status: String,
  },
  data() {
    return {
      dateFrom: "",
      dateTo: "",
      modalTitle: "",
      style: `backgroundColor:${this.bgColor}`,
    };
  },
  methods: {
    closeModal() {
      this.$emit("handleClose");
    },
    confirmModal() {
      this.$emit("handleConfirm", {
        id: this.id,
        from: this.dateFrom,
        to: this.dateTo,
        title: this.modalTitle,
        bgColor: this.bgColor,
        status: this.status,
      });
    },
    deleteModal() {
      this.$emit("handleDelete", this.id);
    },
  },
  created() {
    this.dateFrom = this.from;
    this.dateTo = this.to;
    this.modalTitle = this.title;
  },
};
</script>

<style lang="scss" scoped>
.input {
  align-items: center;
  background-color: rgba(0, 0, 0, 0.2);
  display: flex;
  height: 100%;
  justify-content: center;
  left: 0;
  padding: 20px;
  position: fixed;
  top: 0;
  width: 100%;
  & .modal {
    background: rgb(67, 71, 75);
    border-radius: 8px;
    box-shadow: 0 14px 28px rgba(0, 0, 0, 0.25), 0 10px 10px rgba(0, 0, 0, 0.22);
    display: flex;
    flex-direction: column;
    width: 600px;
    height: 220px;
    & input {
      background: none;
      border: none;
      border-bottom: 1px solid rgba(255, 255, 255, 0.2);
      color: whitesmoke;
      height: 30px;
      margin: 0 1rem;
    }
    & .date {
      align-items: center;
      color: rgba(255, 255, 255, 0.5);
      display: flex;
      font-size: 0.8rem;
      justify-content: space-between;
      margin-left: 1rem;
      width: 50%;
      & input {
        color: whitesmoke;
      }
    }
    & .title {
      margin-top: 1rem;
      width: 550px;
      min-height: 30px;
    }
    & .modalHeader {
      display: flex;
      justify-content: space-between;
      padding: 1rem;
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
      & .closeBtn {
        background: none;
        border: none;
        color: whitesmoke;
        cursor: pointer;
        font-size: 0.8rem;
      }
    }
    & .btnWrapper {
      padding: 1rem;
      display: flex;
      justify-content: space-between;
      & button {
        background: none;
        border: none;
        color: whitesmoke;
        cursor: pointer;
        font-size: 0.8rem;
      }
      & .rightBtn {
        display: flex;
        & .closeBtn {
          color: rgba(255, 255, 255, 0.5);
        }
      }
      & .deleteBtn {
        color: orangered;
      }
    }
  }
}
</style>
