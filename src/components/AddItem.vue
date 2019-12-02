<template>
  <div class="add-item">
    <div v-if="isHiddenForm" class="button-container" @click="changeModeInput">
      <i class="material-icons">playlist_add</i>
    </div>

    <div v-else class="form-container">
      <form class="form-box" @submit.prevent="addItem">
        <input
          class="form-input"
          type="text"
          v-model="title"
          :placeholder="placeholder"
        />
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: "AddItem",
  data: () => {
    return {
      title: "",
      isHiddenForm: true
    };
  },
  props: {
    placeholder: String
  },
  methods: {
    changeModeInput() {
      this.isHiddenForm = false;
    },

    addItem() {
      this.isHiddenForm = true;
      if (!this.title) return;

      this.$emit("add", this.title);
      this.title = "";
    }
  }
};
</script>

<style lang="scss" scoped>
.add-item {
  .button-container {
    width: 100%;
    height: 40px;
    display: table;
    text-align: center;
    cursor: pointer;

    i {
      display: table-cell;
      vertical-align: middle;
    }

    &:hover {
      background-color: #f5f5f5;
    }
  }

  .form-container {
    padding: 0 8px;
    background-color: #f5f5f5;
  }

  .form-box {
    width: 100%;
  }

  .form-input {
    padding: 0;
    width: 100%;
    height: 40px;
    color: inherit;
    font-family: inherit;
    font-size: 100%;
    background-color: inherit;
    border: none;
    outline: none;
  }
}
</style>
