<template>
<div :class="{'select-file' : isActive}" @focus="addSelectFile" @blur="removeSelectFile" tabindex="1">
    <span>
        <slot name="icon"></slot>
    </span>
    <slot name="name"></slot>
</div>
</template>

<script>
import FileTree from "../FileTree/FileTree.vue";

export default {
  name: "LinkTree",
  extends: FileTree,
};
</script>

<style scoped></style>
