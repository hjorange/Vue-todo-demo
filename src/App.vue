<template>
  <div class="todoapp">
    <TodoHeader :arr="list" @enter="enter"/>
    <TodoMain :arr="newList" @del="del"/>
    <TodoFooter :arr="list" :active="active" @onactive="onactive" @clear="clear"/>
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue'
import TodoMain from './components/TodoMain.vue'
import TodoFooter from './components/TodoFooter.vue'
export default {
  data () {
    return {
      active: '',
      list: JSON.parse(localStorage.getItem('list')) || []
    }
  },
  components: {
    TodoHeader,
    TodoMain,
    TodoFooter
  },

  computed: {
    newList () {
      if (this.active === 'undone') {
        return this.list.filter(item => !item.isDone)
      } else if (this.active === 'done') {
        return this.list.filter(item => item.isDone)
      } return this.list
    }
  },

  watch: {
    list: {
      deep: true,
      handler () {
        localStorage.setItem('list', JSON.stringify(this.list))
      }
    }
  },

  methods: {
    enter (taskname) {
      const id = this.list.length ? this.list[this.list.length - 1].id + 1 : 100
      const flag = this.list.some(item => item.name === taskname)
      flag ? alert('数据重复') : this.list.push({
        id,
        name: taskname
      })
    },
    onactive (active) {
      this.active = active
    },
    clear (undone) {
      this.list = undone
    },
    del (id) {
      const index = this.list.findIndex(item => item.id === id)
      this.list.splice(index, 1)
    }
  }
}
</script>

<style scoped>

</style>
