<template>
  <li class="todo-item">
    <span id="todo-title">{{ title }}</span>
    <div class="finish-checkbox" @click="ChangeState">
      <div v-if="itemState" class="finish-solid"></div>
    </div>
  </li>
</template>

<script>
export default {
  name: "TodoItem",
  props: {
    title: String,
    state: Boolean,
    number: Number,
  },
  data() {
    return {
      itemState: this.state,
    };
  },
  mounted() {
    console.log(this.state);
  },
  methods: {
    ChangeState() {
      console.log(document.getElementsByClassName("todo-item"));
      const t = document.getElementsByClassName("todo-item")[this.number - 1];
      this.itemState = !this.itemState;
      let i = JSON.parse(localStorage.getItem("items"));
      i[this.number - 1].state = this.itemState;
      localStorage.setItem("items", JSON.stringify(i));
      if (this.itemState == true) {
        t.style.textDecoration = "line-through";
        t.style.color = "var(--disabled-text)";
      } else {
        t.style.textDecoration = "none";
        t.style.color = "#000";
      }
    },
  },
};
</script>

<style scoped>
* {
  user-select: none;
}
li {
  display: flex;
  box-shadow: -10px 10px 10px 0px var(--dark-background);
  background-color: var(--base-background);
  border-radius: 3px;
  padding-inline: 10px;
  transition: 0.5s;
  margin-top: 10px;
  height: 35px;
  line-height: 35px;
  /* text-decoration: line-through;
  color: var(--disabled-text); */
}

li:hover {
  background-color: var(--hover-background);
}

#todo-title {
  width: 800px;
  height: 35px;
  font-size: 20px;
  font-weight: 700;
  overflow: auto;
}

.finish-checkbox {
  display: flex;
  align-items: center;
  justify-content: center;
  transition: 0.5s;
  width: 20px;
  height: 20px;
  border-radius: 20px;
  background-color: var(--dark-background);
  float: right;
  margin-right: 10px;
  margin-top: 7.5px;
}

.finish-checkbox:hover {
  cursor: pointer;
  background-color: var(--hover-dark-background);
}

.finish-solid {
  width: 10px;
  height: 10px;
  border-radius: 10px;
  background-color: var(--base-fill);
}
</style>
