<template>
  <div id="box">
    <div id="top-information">
      <p id="left-todos">
        You have <span id="left-todo-num">{{ leftTodoNum }}</span> Todos left.
      </p>
      <p id="today">
        Now is <span style="color: #000">{{ nowDate }}</span>
      </p>
    </div>
    <TodoList style="margin-top: 30px" :items="items"></TodoList>
    <AddNewItem
      style="margin-top: 30px"
      @showWarning="ShowWarning"
      @update="UpdateTodos"
    ></AddNewItem>
  </div>
</template>

<script setup>
import TodoList from "./TodoList.vue";
import AddNewItem from "./AddNewItem.vue";
</script>

<script>
export default {
  components: { TodoList, AddNewItem },
  name: "TodoListBox",
  data() {
    return {
      nowDate: null,
      leftTodoNum: 0,
      items: null,
    };
  },
  mounted() {
    this.GetNowTime();
    setInterval(() => {
      this.GetNowTime();
    }, 1000);
    this.InitItems();
    this.UpdateTodos();
  },
  methods: {
    ShowWarning() {
      this.$emit("showWarningToApp");
    },
    GetNowTime() {
      var d = new Date();
      var nowYear = d.getFullYear();
      var nowMonth = d.getMonth() + 1;
      var nowDay = d.getDate();
      var nowHour = d.getHours();
      var nowMinute = d.getMinutes();
      var nowSecond = d.getSeconds();
      if (nowMonth < 10) {
        nowMonth = "0" + nowMonth;
      }
      if (nowDay < 10) {
        nowDay = "0" + nowDay;
      }
      if (nowHour < 10) {
        nowHour = "0" + nowHour;
      }
      if (nowMinute < 10) {
        nowMinute = "0" + nowMinute;
      }
      if (nowSecond < 10) {
        nowSecond = "0" + nowSecond;
      }
      this.nowDate =
        nowYear +
        "-" +
        nowMonth +
        "-" +
        nowDay +
        " " +
        nowHour +
        ":" +
        nowMinute +
        ":" +
        nowSecond;
    },
    InitItems() {
      let i;
      if (localStorage.getItem("items")) {
        var initedItems = [];
        i = JSON.parse(localStorage.getItem("items"));
        var index = 0;
        console.log(i);
        localStorage.removeItem("items");
        for (var x = 0; x < i.length; x++) {
          if (i[x].state == false) {
            initedItems.push({
              title: i[x].title,
              state: false,
              number: index + 1,
            });
            index++;
          }
        }
        localStorage.setItem("items", JSON.stringify(initedItems));
      }
    },
    UpdateTodos() {
      let i;
      if (localStorage.getItem("items")) {
        i = localStorage.getItem("items");
        this.items = JSON.parse(i);
        this.leftTodoNum = this.items.length;
      } else {
        this.leftTodoNum = 0;
      }
      console.log(this.leftTodoNum);
      const leftNumText = document.getElementById("left-todo-num");
      if (this.leftTodoNum >= 10) leftNumText.style.color = "#F56C6C";
      else if (this.leftTodoNum > 3 && this.leftTodoNum < 10)
        leftNumText.style.color = "#E6A23C";
      else leftNumText.style.color = "#67C23A";
    },
  },
};
</script>

<style scoped>
ul {
  margin-top: 30px;
  padding-inline: 50px;
  list-style: none;
}

li {
  height: 40px;
  display: flex;
  align-items: center;
}

#top-information {
  display: flex;
}

#left-todos {
  font-size: 20px;
  margin-left: 50px;
  color: var(--regular-text);
}

#today {
  font-size: 20px;
  color: var(--regular-text);
  margin-left: 300px;
}

#box {
  height: 550px;
  padding-inline: 50px;
}
</style>
