<template>
  <header class="header">
    <h1>todos</h1>
    <input v-model="all" id="toggle-all" class="toggle-all" type="checkbox" >
    <label for="toggle-all"></label>
    <input
      class="new-todo"
      placeholder="输入任务名称-回车确认"
      autofocus
      @keyup.enter="enter"
      v-model.trim="name"
    />
  </header>
</template>

<script>
export default {
  data () {
    return {
      name: ''
    }
  },
  props: ['arr'],
  methods: {
    enter () {
      this.name.length ? this.$emit('enter', this.name) : alert('请输入内容')
      this.name = ''
    }
  },
  computed: {
    all: {
      get () {
        return this.arr.every(item => item.isDone)
      },
      set (check) {
        this.arr.forEach(item => {
          return item.isDone = check
        })
      }
    }
  }
}
</script>
