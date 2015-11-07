<template>
  <nav class="navbar navbar-light bg-faded">
    <div class="container">
      <a class="navbar-brand" href="#">Tasks</a>
    </div>
  </nav>
  <div class="container m-t">
    <form class="m-b" @submit="addTask">
      <input type="text" class="form-control" placeholder="I need to..." v-model="newTask" />
    </form>

    <div class="row">
      <div class="col-lg-12">
        <section  v-show="tasksInProcess.length">
          <h2 class="m-b">{{ tasksInProcess.length }} {{ tasksInProcess.length | pluralize 'Task' }}</h2>

          <ul class="list-group">
            <task v-for="task in tasksInProcess" :task="task"></task>
          </ul>
        </section>

        <section v-show="completedTasks.length">
          <h2 class="m-b m-t">{{ completedTasks.length }} {{ completedTasks.length | pluralize 'Completed Task' }}</h2>

          <ul class="list-group">
            <task v-for="task in completedTasks" :task="task"></task>
          </ul>
        </section>
      </div>
    </div>
  </div>
</template>

<script>
  var Task = require('./task.vue');

  module.exports = {
    components: {
      task: Task
    },
    data: function () {
      return {
        newTask: '',
        tasks: []
      }
    },
    computed: {
      tasksInProcess: function() {
        return this.tasks.filter(function(task) {
          return !task.completed;
        });
      },
      completedTasks: function() {
        return this.tasks.filter(function(task) {
          return task.completed;
        });
      }
    },
    methods: {
      addTask: function(e) {
        e.preventDefault();

        this.tasks.push({
          title: this.newTask,
          completed: false
        });

        this.newTask = '';
      }
    },
    events: {
      taskRemoved: function(task) {
        this.tasks.$remove(task);
      }
    }
  }
</script>
