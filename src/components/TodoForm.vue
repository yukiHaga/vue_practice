<template>
  <h3>My Todo</h3>
  <!-- v-modelも要はは、同期させているだけ。-->
  <input v-model="message" placeholder="Input here...">
  <button v-on:click="onSubmitFactory">ADD</button>
</template>

<script>
export default {
  data () {
    return {
      message: ""
    }
  },
  emits: ["submit"],
  methods: {
    onSubmitFactory () {
      if (this.message === '') return;
      this.$emit('submit', this.message);
      this.message = '';
    }
  }
}
</script>
