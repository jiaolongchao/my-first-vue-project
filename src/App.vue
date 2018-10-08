<template>
  <div id="app">
    <img src="./assets/logo.png">
    <h1 v-text='title'></h1>
    <ul>
      <li v-for="(item,index) in items" v-bind:key='index' v-bind:class='{finished:item.isFinished}' v-on:click='toggleFinish(item)'>        
        {{item.label}}
      </li>
    </ul>
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld";

export default {
  name: "App",
  components: {
    HelloWorld
  },
  data: function() {
    return {
      title: "this is todo list",
      items: [
        {
          label: "coding",
          isFinished: true
        },
        {
          label: "working",
          isFinished: false
        }
      ]
    };
  },
  methods: {
    toggleFinish: function() {
      console.log((item.isFinished = !item.isFinished));
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.finished {
  text-decoration: underline;
}
</style>
