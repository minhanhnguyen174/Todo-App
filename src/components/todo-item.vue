<template>
<div>
  <b-list-group-item v-for="(todoItem, index) in todoItems" :key="index" class="my-1 d-flex justify-content-between align-items-center">
    <div v-show="todoItem.edit == false">
      <label @dblclick="todoItem.edit = true">{{index+1}}. {{todoItem.name}}</label>
    </div>
    <input v-show="todoItem.edit == true" v-model="todoItem.name" v-on:blur="todoItem.edit=false; $emit('update')" @keyup.enter="todoItem.edit=false;
            $emit('update')" />

    <div class="d-flex flex-row align-items-center">
      <b-form-checkbox class="" :id="index" v-model="todoItem.checked" @change="doneTask(todoItem)"></b-form-checkbox>
      <b-btn class="mr-2" size="sm" text="Button" variant="primary" @click="deleteTask(todoItem)">delete</b-btn>
    </div>
  </b-list-group-item>

</div>
</template>

<script>
  export default {
    name: 'TodoApp',
    props: {
      todoItem: Object,
      todoItems: Array,
      todoDone: Array,
      
    },
    methods: {

      deleteTask: function (e) {
        this.todoItems.splice(this.todoItems.indexOf(e), 1);

        var doneList = this.todoDone;
        if (doneList.length > 0 && e.checked == true)
          doneList.splice(doneList.indexOf(e), 1)
      },

      doneTask: function (e) {
        if (e.checked == false)
          this.todoDone.push({
            id: e.id,
            name: e.name,
            checked: e.checked
          });
        else
          this.todoDone.splice(this.todoDone.indexOf(e), 1);
      },

      editTask: function (todoItem) {
        this.editedTask = todoItem;
      }
    }
  }
</script>