<template>
  <div id="app">
    <!-- <router-view/> -->
    <h1 v-text="title"></h1>
    <input v-model="newItem" v-on:keyup.enter="addNew">
    <ul>
      <li v-for="item in items" v-bind:class="{isFinished:item.isFinished}" :key="item" v-on:click="toggleFinish(item)">
        {{item.lable}}
      </li>
    </ul>
    <components-a msgfromcomponent = "you die!" v-on:child-tell-to-me="tell"></components-a>
    <p>child tell me:{{ childWords }}</p>
  </div>
</template>

<script>
import WindowItems from './store.js'
import ComponentsA from './components/ComponentsA'
export default {
  name: 'App',
  data () {
    return {
      title: 'this is a todo list',
      items: WindowItems.fetch(),
      newItem: '',
      childWords: ''
    }
  },
  // 引入其它组件需要注册，否则无法使用
  components: {
    ComponentsA
  },
  methods: {
    toggleFinish (item) {
      item.isFinished = !item.isFinished
    },
    addNew () {
      this.items.push({
        lable: this.newItem,
        isFinished: false
      })
      this.newItem = ''
    },
    tell (message) {
      this.childWords = message
    }
  },
  watch: {
    items: {
      handler: function (items) {
        WindowItems.save(items)
      },
      deep: true
    }
  }
}
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
.isFinished {
  color: red;
}
ul {
  list-style: none;
  padding: 0;
}
li {
  height: 30px;
}
</style>
