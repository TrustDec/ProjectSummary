<template>
  <div id="app">
    <h1 v-text="title"></h1>
    <ul>
      <li v-for="item in items" v-bind:class="[finished,liClass]">
        {{item.label}}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data: function(){
    return {
      title: 'this is a todo list',
      items: [{
        label: 'coding',
        isFinished: false
      },
      {
        label: 'walking',
        isFinished:true
      }
      ],
      liClass:"liClass",
      finished:"finished"
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
.liClass{
  font-size: 20px;
}
.finished {
  color:red;
  font-weight: bold;
}
</style>
