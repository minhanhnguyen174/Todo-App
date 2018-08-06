<template>
  <div id="app">
    <!-- <TodoApp msg="Todo app"/> -->
    <b-container class="app-container mt-5">
      <b-row>
        <b-col cols="5" class="mx-auto m-shadow">
          <h1 class="title-wrap">
            <b-badge class="title">TODO-APP</b-badge>
          </h1>

          <div class="my-4">
            <h5>You have
              <strong>{{done.length}}/{{items.length}}</strong> uncompleted.</h5>
          </div>
            
          <b-input-group v-for="size in ['']" :key="size" :size="size" class="mb-2">
            <b-form-input v-model="newTask" />
            <b-input-group-append>
              <b-btn size="sm" text="Button" variant="primary" @click="addTask">Add</b-btn>
            </b-input-group-append>
            <b-input-group-append>
              <b-btn size="sm" text="Button" variant="danger" @click="deleteAll">Delete All</b-btn>
            </b-input-group-append>
          </b-input-group>

          <b-list-group>

            <!-- item mới sau khi thêm sẽ hiển thị ở đây -->
            <todoitems :todoItem="item" :todoItems="items" :todoDone="done"/>

          </b-list-group>
        </b-col>

      </b-row>
    </b-container>
  </div>
</template>
<script>
  // import HelloWorld from './components/HelloWorld.vue'
  // import TodoApp from './components/todo-app.vue';
  import todoitems from './components/todo-items.vue';
  import Vue from 'vue'
  import BootstrapVue from "bootstrap-vue"
  import "bootstrap/dist/css/bootstrap.min.css"
  import "bootstrap-vue/dist/bootstrap-vue.css"

  Vue.use(BootstrapVue)

  export default {
    name: 'app',
    components: {
      todoitems
    },
    data: function () {
      return {
        items: [],
        newTask: "",
        done: []
      }
    },
    methods: {
      addTask: function () {
        if (this.newTask != "") {
          this.items.push({
            id: this.items.length + 1,
            name: this.newTask,
            checked: false,
            edit: false
          });
          this.newTask = "";
        } else
          alert("Please type your task :)")
      },

      deleteAll: function () {
        this.items = [];
        this.done = [];
      }
    },

    
  }
</script>

<style lang="scss">
  @import './assets/scss/todo-app.scss';
</style>