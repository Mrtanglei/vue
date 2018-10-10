<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h3>{{ msgfromcomponent }}</h3>
    <button v-on:click="clicka">Click!</button>
  </div>
</template>

<script>
export default {
  name: 'ComponentsA',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  // 注册属性，否则在父组件中无法传递给子组件
  props: [
    'msgfromcomponent'
  ],
  methods: {
    clicka () {
      alert(this.msgfromcomponent)
      this.$emit('child-tell-to-me', 'hei hei hei')
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1，h3{
  font-weight: normal;
}
</style>
