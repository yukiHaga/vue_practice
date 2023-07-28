<template>
  <!-- v-onはonClickみたいなやつ, 子で指定した関数をemitを使って呼び出せる -->
  <TodoForm v-on:submit="onSubmit" />
  <h5>Todo List</h5>
  <ul>
    <!-- v-bindはvue.jsのデータをプロップスで渡すために使う。vue.jsのデータじゃないなら、v-on使わなくても普通にプロップスで渡せる -->
    <!-- v-bindはstateなどの動的な値を渡す時に使う。静的な値なら普通にpropsで渡せる -->
    <!-- vue.jsでliにforを指定するのにめちゃ違和感を感じる。reactではforの中身を複数生成するのであって、 liより上の階層の要素にforを指定するのが自然なんよな -->
    <!-- vue.jsには要素の属性に{}を指定するのができないな -->
    <TodoItem v-for="todo in todos" v-bind:key="todo.id" v-bind:todo="todo" v-on:click="onClickDelete" />
  </ul>
</template>

<script>
import TodoForm from './components/TodoForm';
import TodoItem from './components/TodoItem';
import { Todo } from "./model/todo"

// Vue.jsではdataオプションでuseStateが実現できる
export default {
  // nameはこのコンポーネントの名前
  name: 'App',
  // このコンポーネント内で使用する別のコンポーネントを指定している
  // HelloWorldというコンポーネントがこのAppコンポーネント内で使用されることを示しています。
  // これにより、HelloWorldコンポーネントがAppコンポーネントのテンプレート内で使用可能になります。
  data() {
    return {
      todos: []
    }
  },
  components: {
    TodoForm,
    TodoItem,
  },
  methods: {
    onSubmit(message) {
      // このidのロジックはクラスに隠蔽した方が良い
      const id = this.todos[this.todos.length - 1]?.id ? this.todos[this.todos.length - 1].id + 1 : 1
      const newTodo = new Todo(id, message)
      this.todos = [...this.todos, newTodo];
    },
    onClickDelete(id) {
      this.todos = this.todos.filter((todo) => todo.id !== id);
    },
  }
}
</script>
