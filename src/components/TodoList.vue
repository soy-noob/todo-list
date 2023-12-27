<template>
  <div>
    <ul>
      <TodoItem
        v-for="(item, index) in items"
        :title="item.title"
        :state="item.state"
        :number="item.number"
        :key="index"
      ></TodoItem>
    </ul>
  </div>
</template>

<script>
import TodoItem from "./TodoItem.vue";
export default {
  components: {
    TodoItem,
  },
  name: "TodoList",
  props: {
    items: Array,
  },
  data() {
    return {};
  },
};
</script>

<style scoped>
ul {
  height: 400px;
  overflow: auto;
  box-shadow: -10px 10px 10px 0px var(--base-background);
  list-style: none;
  padding-inline: 40px;
  padding-bottom: 40px;
}
</style>
