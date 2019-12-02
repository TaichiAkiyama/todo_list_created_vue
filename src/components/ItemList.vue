<template>
  <div class="item-list">
    <div class="item-container" v-for="item in items" :key="item.id">
      <Item :data="item" @delete="deleteItem" />
    </div>
  </div>
</template>

<script>
import Item from "./Item";

export default {
  name: "ItemList",
  components: { Item },
  props: {
    items: Array
  },
  computed: {},
  methods: {
    deleteItem(id) {
      const index = this.items.findIndex(item => {
        return item.id === id;
      });
      this.items.splice(index, 1);
    }
  }
};
</script>

<style lang="scss" scoped>
.item-list {
  .item-container {
    border-top: 1px solid #808080;

    &:last-child {
      border-bottom: 1px solid #808080;
    }
  }
}
</style>
