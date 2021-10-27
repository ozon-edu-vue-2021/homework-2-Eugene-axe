<template>
  <div>
    <span @click.stop="toggleIsShow">
      <directory-close v-if="!isShow" />
      <directory-open v-else />
      {{ child.name }}
    </span>
    <item-tree
      :childrens="child.contents"
      v-if="isShow"
      :parentPath="parentPath + child.name"
    />
  </div>
</template>

<script>
import DirectoryClose from "../icons/directoryClose.vue";
import DirectoryOpen from "../icons/directoryOpen.vue";
import EventBus from "../EventBus/EventBus";
import {GET_TREE_FULL_PATH} from '../../constants/events'

export default {
  name: "DirectoryTree",
  data: () => ({
    isShow: false,
  }),
  props: {
    child: {
      type: Object,
    },
    parentPath: {
      type: String,
    },
  },
  components: {
    ItemTree: () => import("../ItemTree/ItemTree.vue"),
    DirectoryClose,
    DirectoryOpen,
  },
  computed: {
    fullPath() {
      return this.parentPath + this.child.name;
    },
  },
  methods: {
    toggleIsShow() {
      this.isShow = !this.isShow;
      this.changeFullPath();
    },
    changeFullPath() {
      EventBus.$emit(GET_TREE_FULL_PATH, this.isShow ? this.fullPath : this.parentPath);
    },
  },
};
</script>

<style scoped></style>
