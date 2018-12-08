<template>

<div id="app">
<input type="text" v-model="msg" @keydown="add($event)"/>

 <h3>进行中</h3>
<ul>
  <li v-for="(item,i) in list" :key="i" v-if="!item.check">
    <input type="checkbox" v-model="item.check" @change='saveList()'/>
     {{item.name}}
     <button @click="del(i)">删除</button>
  </li>
  
</ul>

<hr>

<h3>已完成</h3>
<ul class="f">
  <li v-if="item.check" v-for="(item,i) in list" :key="i">
     <input type="checkbox" v-model="item.check"/>
     {{item.name}}
    <button @click="del(i)">删除</button>
  </li>
   
</ul>

</div>

</template>

<script>
import storage from "./model/storage.js";

export default {
  data() {
    return {
      msg: "",
      list: []
    };
  },
  mounted() {
    var list = storage.get("list");
    if (list) {
      this.list = list;
    }
  },
  methods: {
    add(e) {
      if (e.keyCode == 13) {
        this.list.push({ name: this.msg, check: false });
        storage.set("list", this.list);
      }
    },
    del(i) {
      this.list.splice(i, 1);
      storage.set("list", this.list);
    },
    saveList() {
      storage.set("list", this.list);
    }
  }
};
</script>

<style lang="scss">
  .f{
    background-color: beige
  }
</style>

