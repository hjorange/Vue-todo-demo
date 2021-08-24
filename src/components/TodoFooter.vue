<template>
  <footer class="footer">
    <span class="todo-count">剩余<strong>数量值:{{count}}</strong></span>
    <ul class="filters">
      <li>
        <a @click="$emit('onactive', 'all')" :class="{selected:active==='all'}" href="javascript:;" >全部</a>
      </li>
      <li>
        <a @click="$emit('onactive', 'undone')" :class="{selected:active==='undone'}" href="javascript:;">未完成</a>
      </li>
      <li>
        <a @click="$emit('onactive', 'done')" :class="{selected:active==='done'}" href="javascript:;" >已完成</a>
      </li>
    </ul>
    <button class="clear-completed" @click="btn">清除已完成</button>
  </footer>
</template>

<script>
export default {
  props: ['arr', 'active'],
  computed: {
    count () {
      return this.arr.filter(item => !item.isDone).length
    }
  },
  methods: {
    btn () {
      const undone = this.arr.filter(item => !item.isDone)
      this.$emit('clear', undone)
    }
  }
}
</script>
