<template>
  <div id="app">
    <h1 v-text="title"></h1>
    <input v-model="newItem" v-on:keyup.enter="addNew">
    <ul>
      <li v-for="item in items" v-bind:class="{finished:item.isFinished}" v-on:click="toggleFinish(item)">
        {{item.label}}
      </li>
    </ul>
    <p>child tell me: <span class="childWords">{{ childWords }}</span></p>
    <Hello msgfromfather='you die!'  v-on:child-tell-me-something="listenToMyBoy"></Hello>
  </div>
</template>

<script>
import Store from './components/store';
import Hello from './components/Hello';
export default {
  data: function(){
    return {
      title: 'this is a todo list',
      items: Store.fetch(),
      newItem:"",
      childWords:''
    }
  },
  components:{Hello},
  watch: {
    items:{
      handler:function(items){
        Store.save(items);
      },
      deep:true
    }
  },
  events: {
    'child-tell-me-something':function(msg){
      this.childWords=msg;
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
        //console.log(this);
         this.$emit('onAddnew',this.items); //2.0:丢弃
        //Store.save();
      },
      listenToMyBoy:function(msg){
       this.childWords = msg;
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
.childWords {
  color: #42b983;
  font-weight: bold;
}
</style>
