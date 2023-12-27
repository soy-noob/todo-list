<template>
  <div id="add-box">
    <input type="text" id="new-item" />
    <div id="add-btn" @click="AddNewItem">Add</div>
  </div>
</template>

<script>
import TodoItem from "./TodoItem.vue";
export default {
  components: { TodoItem },
  name: "AddNewItem",
  data() {
    return {};
  },
  methods: {
    AddNewItem() {
      if (document.getElementById("new-item").value == "") {
        this.$emit("showWarning");
        return;
      }
      let nowItems;
      if (localStorage.getItem("items")) {
        nowItems = JSON.parse(localStorage.getItem("items"));
        nowItems.push({
          title: document.getElementById("new-item").value,
          state: false,
          number: nowItems.length + 1,
        });
      } else {
        nowItems = [
          {
            title: document.getElementById("new-item").value,
            state: false,
            number: 1,
          },
        ];
      }
      localStorage.setItem("items", JSON.stringify(nowItems));
      document.getElementById("new-item").value = "";
      this.$emit("update");
    },
  },
};
</script>

<style scoped>
#add-box {
  width: 900px;
  height: 80px;
  display: flex;
  align-items: center;
}

#new-item {
  transition: 0.5s;
  width: 820px;
  height: 40px;
  border: none;
  background-color: var(--base-background);
  font-size: 20px;
  padding-inline: 10px;
}

#new-item:focus {
  outline: none;
  background-color: var(--dark-background);
}

#add-btn {
  transition: 0.5s;
  width: 100px;
  height: 40px;
  text-align: center;
  line-height: 40px;
  color: #fff;
  background-color: var(--light-fill);
  margin-left: 30px;
}

#add-btn:hover {
  cursor: pointer;
  background-color: var(--dark-fill);
}
</style>
