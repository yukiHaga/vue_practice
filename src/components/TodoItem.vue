<template>
  <li>
    <!-- 要素の中なら、{{}}でデータを参照できる -->
    {{ todo.message }}
    <button v-on:click="onClickFactory">delete</button>
  </li>
</template>

<script>
export default {
  name: "TodoItem",
  // vue.jsでのv-bindのpropsの受け取り方
  props: ["todo"],
  emits: ["click"],
  methods: {
    // thisでpropsのデータをmethodsから参照できる
    onClickFactory () {
      this.$emit('click', this.todo.id);
    }
  }
}
</script>
