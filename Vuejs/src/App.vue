<template>
  <div id="app">
    <h1 v-text="title"></h1>
    <input v-model="newItem" v-on:keyup.enter="addNew">
    <ul>
      <li v-for="item in items" v-bind:class="{finished:item.isFinished}" v-on:click="toggleFinish(item)">
        {{item.label}}
      </li>
    </ul>
  </div>
</template>

<script>
import Store from './components/store.js';
export default {
  data: function(){
    return {
      title: 'this is a todo list',
      items: Store.fetch(),
      newItem:"",
    }
  },
  watch: {
    items:{
      handler:function(items){
        Store.save(items);
      },
      deep:true
    }
  },
  methods: {
     toggleFinish:function(item){
        console.log(item.isFinished = !item.isFinished);
      },
      addNew:function(){
        this.items.push({
          label:this.newItem,
          isFinished:false
        });
        this.newItem="";
        Store.save();
      }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.finished {
  color:red;
  font-size: 20px;
  font-weight: bold;
}
li {
  color:green;
  font-size: 20px;
  font-weight: bold;
}
</style>
