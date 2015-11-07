<template>
  <li class="list-group-item">
    {{ task.title }}
    <div class="btn-group pull-right" role="group" aria-label="Actions" v-show="!task.completed">
      <button type="button"
        class="btn btn-success-outline btn-sm"
        @click="complete(task)">&#10004;</button>

      <button type="button"
        class="btn btn-danger-outline btn-sm"
        @click="remove(task)">X</button>
    </div>
  </li>
</template>

<script>
  module.exports = {
    props: ['task'],
    methods: {
      remove(task) {
        this.$dispatch('taskRemoved', task);
      },
      complete: function(task) {
        task.completed = true;
      }
    }
  }
</script>
