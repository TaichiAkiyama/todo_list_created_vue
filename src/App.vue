<template>
  <div id="app">
    <div class="todo-list">
      <div class="title">Todo List</div>

      <div class="form">
        <AddItem placeholder="Input todo..." @add="addItem" />
      </div>

      <div class="list">
        <ItemList :items="items" />
      </div>
    </div>
  </div>
</template>

<script>
import AddItem from "./components/AddItem.vue";
import ItemList from "./components/ItemList.vue";

export default {
  name: "app",
  components: {
    AddItem,
    ItemList
  },
  data: () => {
    return { items: [] };
  },
  methods: {
    addItem(title) {
      let id = 1;
      if (this.items.length > 0) {
        id =
          Math.max.apply(
            null,
            this.items.map(item => item.id)
          ) + 1;
      }

      this.items.push({
        id,
        title,
        isChecked: false
      });
    }
  }
};
</script>

<style lang="scss">
#app {
  width: 100%;
  color: #696969;
  font-size: 18px;
}

.todo-list {
  padding: 16px;
  width: 600px;
  border: 1px solid #696969;
}

.title {
  font-size: 24px;
  text-align: center;
}

.form {
  margin-top: 16px;
}
</style>
