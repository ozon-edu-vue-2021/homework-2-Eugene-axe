<template>
  <ul>
    <li v-for="child in childrens" :key="child.name">
      <directory-tree v-if="isDirectory(child)" :child="child" :parentPath="parentPath + '/'" />
      <file-tree v-else-if="isFile(child)" :child="child" :parentPath="parentPath + '/'">
        <template v-slot:icon>
          <file-icon />
        </template>
        <template v-slot:name> {{ child.name }}</template>
      </file-tree>
      <file-tree v-else-if="isLink(child)" :child="child" :parentPath="parentPath + '/'">
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
import {TYPE_DIRECTORY , TYPE_FILE, TYPE_LINK} from '../../constants/types'; 

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
  methods: {
    isDirectory(child){
      return child.type === TYPE_DIRECTORY;
    },
    isFile(child){
      return child.type === TYPE_FILE;
    },
    isLink(child){
      return child.type === TYPE_LINK;
    },
  }
};
</script>

<style scoped></style>
