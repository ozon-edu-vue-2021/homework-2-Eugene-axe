<template>
  <div id="app">
    <h3>{{fullPath}}</h3>
    <item-tree :childrens="DataTree" :parentPath="'root'"/>
  </div>
</template>

<script>
import DataTree from '../public/static/node_modules.json';
import EventBus from './EventBus';
import {GET_TREE_FULL_PATH} from './constants/events';


export default {
  name: 'App',
  data : () =>({
    DataTree : [DataTree],
    fullPath : 'root/',
  }),
  components : {
    ItemTree : () => import('./components/ItemTree/ItemTree.vue')
  },
  created(){
    EventBus.$on(GET_TREE_FULL_PATH , path =>{
      this.fullPath = path;
    })
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin: 0 auto;
  width: 80%;
  background-color: rgb(212, 208, 208);
  user-select: none;
}
ul {
  list-style-type: none;
}
</style>
