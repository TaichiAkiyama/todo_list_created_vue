<template>
  <div class="item" :class="classes">
    <div class="container">
      <div v-if="isPreview" class="preview">
        <div class="preview-content">
          <div
            v-if="isChecked"
            class="preview-checkbox-checked"
            @click="unchecked"
          />
          <div v-else class="preview-checkbox" @click="checked" />

          <span class="preview-title" @click="changeModeEditable">
            {{ data.title }}
          </span>
        </div>

        <div class="preview-buttons">
          <i class="material-icons delete-button" @click="deleted"
            >restore_from_trash</i
          >
        </div>
      </div>

      <div v-else class="editable">
        <div class="preview-checkbox-disabled" />
        <form class="editable-form" @submit.prevent="edited">
          <input class="editable-title" type="text" v-model="data.title" />
        </form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Item",
  data: () => {
    return {
      mode: "preview"
    };
  },
  props: {
    data: Object
  },
  computed: {
    classes: function() {
      return this.data.status;
    },

    isPreview: function() {
      return this.mode === "preview";
    },

    isChecked: function() {
      return this.data.isChecked;
    }
  },
  methods: {
    changeModePreview() {
      this.mode = "preview";
    },

    changeModeEditable() {
      this.mode = "editable";
    },

    checked() {
      this.data.isChecked = true;
    },

    unchecked() {
      this.data.isChecked = false;
    },

    edited() {
      if (this.data.title === "") this.$emit("delete", this.data.id);
      this.mode = "preview";
    },

    deleted() {
      this.$emit("delete", this.data.id);
    }
  }
};
</script>

<style lang="scss" scoped>
.item {
  .container {
    padding: 0 8px;
    height: 40px;
    line-height: 40px;

    &:hover {
      background-color: #f5f5f5;
    }
  }

  .preview {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .preview-content {
    display: flex;
  }

  .preview-checkbox {
    margin: auto 0;
    width: 15px;
    height: 15px;
    background-color: #fff;
    border: 1px solid #696969;
  }

  .preview-checkbox-checked {
    margin: auto 0;
    position: relative;
    width: 15px;
    height: 15px;
    background-color: #fff;
    border: 1px solid #696969;

    &::after {
      content: "";
      display: block;
      position: absolute;
      top: -5px;
      left: 5px;
      width: 7px;
      height: 14px;
      transform: rotate(40deg);
      border-bottom: 3px solid #000;
      border-right: 3px solid #000;
    }
  }

  .preview-checkbox-disabled {
    margin: auto 0;
    width: 15px;
    height: 15px;
    border: 1px solid #696969;
    background: linear-gradient(
      -45deg,
      #fff 0 48%,
      #696969 48% 52%,
      #fff 52% 100%
    );
  }

  .preview-title {
    margin-left: 8px;
    overflow: hidden;
    white-space: nowrap;
    text-overflow: ellipsis;
  }

  .editable {
    display: flex;
    align-items: center;
  }

  .editable-form {
    width: 95%;
    margin-left: 8px;
  }

  .editable-title {
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

  .preview-buttons {
    display: flex;
    align-items: center;
  }

  .delete-button {
    cursor: pointer;
  }

  .done {
    .preview-checkbox {
      background-color: #000;
    }
  }
}
</style>
