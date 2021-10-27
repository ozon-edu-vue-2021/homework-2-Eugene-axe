<template>
  <ul>
    <li v-for="child in childrens" :key="child.name">
      <directory-tree v-if="child.type === 'directory'" :child="child" :parentPath="parentPath + '/'" />
      <file-tree v-else-if="child.type === 'file'" :child="child" :parentPath="parentPath + '/'">
        <template v-slot:icon>
          <file-icon />
        </template>
        <template v-slot:name> {{ child.name }}</template>
      </file-tree>
      <file-tree v-else-if="child.type === 'link'" :child="child" :parentPath="parentPath + '/'">
        <template v-slot:icon>
          <link-icon />
        </template>
        <template v-slot:name> {{ child.name }}</template>
      </file-tree>
    </li>
  </ul>
</template>

<script>
import FileTree from "../FileTree/FileTree.vue";
import FileIcon from "../icons/FileIcon.vue";
import LinkIcon from "../icons/LinkIcon.vue";

export default {
  name: "ItemTree",
  props: {
    childrens: {
      type: Array,
    },
    parentPath : {
        type : String,
    },
  },
  components: {
    DirectoryTree: () => import("../DirectoryTree/DirectoryTree.vue"),
    FileTree,
    LinkIcon,
    FileIcon,
  },
};
</script>

<style scoped></style>
