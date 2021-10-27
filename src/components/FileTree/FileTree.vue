<template>
  <div
    :class="{ 'select-file': isActive }"
    @focus="addSelectFile"
    @blur="removeSelectFile"
    tabindex="1"
  >
    <span>
      <slot name="icon"></slot>
    </span>
    <slot name="name"></slot>
  </div>
</template>

<script>
import EventBus from "../EventBus/EventBus";
import {GET_TREE_FULL_PATH} from '../../constants/events'

export default {
  name: "FileTree",
  data: () => ({
    isActive: false,
  }),
  props: {
    child: {
      type: Object,
    },
    parentPath: {
      type: String,
    },
  },
  computed: {
    fullPath() {
      return this.parentPath + this.child.name;
    },
  },
  methods: {
    addSelectFile() {
      this.isActive = true;
      this.changeFullPath();
    },
    removeSelectFile() {
      this.isActive = false;
    },
    changeFullPath() {
      EventBus.$emit(GET_TREE_FULL_PATH, this.fullPath);
    },
  },
};
</script>

<style scoped>
.select-file {
  font-weight: 500;
  color: rgb(9, 9, 165);
}
.select-file svg {
  display: inline-block;
  fill: rgb(9, 9, 165);
}
</style>
