<script setup>
import NullInputWarning from "../../todo-list/src/components/NullInputWarning.vue";
import GreetingArea from "../../todo-list/src/components/GreetingArea.vue";
import TodoListBox from "../../todo-list/src/components/TodoListBox.vue";
</script>

<script>
export default {
  components: { NullInputWarning, GreetingArea, TodoListBox },
  data() {
    return {
      warningSetOpacity: 0,
      timeOut: null,
    };
  },
  methods: {
    ShowWarning() {
      clearTimeout(this.timeOut);
      console.log("Y");
      this.warningSetOpacity = 1;
      this.timeOut = setTimeout(() => {
        this.warningSetOpacity = 0;
      }, 2000);
    },
  },
};
</script>

<template>
  <NullInputWarning
    :setOpacity="warningSetOpacity"
    style="position: absolute; top: 20px"
  ></NullInputWarning>
  <div id="container">
    <GreetingArea> </GreetingArea>
    <TodoListBox @showWarningToApp="ShowWarning"></TodoListBox>
  </div>
</template>

<style scoped>
#container {
  width: 1000px;
  height: 700px;
  border-radius: 10px;
  box-shadow: 0 0 10px 0px var(--base-border);
}
</style>
