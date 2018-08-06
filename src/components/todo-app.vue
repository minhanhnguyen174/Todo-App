<template>
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

        <b-list-group>
          <b-list-group-item v-for="(item,index) in items" :key="item.id" class="my-1 d-flex justify-content-between align-items-center">
            <div v-show="item.edit == false">
              <label @dblclick="item.edit = true">{{index+1}}. {{item.name}}</label>
            </div>
            <input v-show="item.edit == true" v-model="item.name" v-on:blur="item.edit=false; $emit('update')" @keyup.enter="item.edit=false;
            $emit('update')" />
            <div class="d-flex flex-row align-items-center">
              <b-form-checkbox class="" :id="index" v-model="item.checked" @change="doneTask(item)"></b-form-checkbox>
              <b-btn class="mr-2" size="sm" text="Button" variant="primary" @click="deleteTask(item)">delete</b-btn>
            </div>
          </b-list-group-item>
        </b-list-group>
      </b-col>

      <b-col cols="5" class="mx-auto m-shadow">
        <h1 class="title-wrap">
          <b-badge class="title">FORM USER</b-badge>
        </h1>

        <b-form>
          <b-form-input id="inputHorizontal"></b-form-input>
        </b-form>

      </b-col>
    </b-row>



  </b-container>
</template>


<script>
  export default {
    name: 'TodoApp',
    props: {

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
      },

      deleteTask: function (e) {
        this.items.splice(this.items.indexOf(e), 1);

        var doneList = this.done;
        if (doneList.length > 0)
          doneList.splice(doneList.indexOf(e), 1)
      },

      doneTask: function (e) {
        if (e.checked == false)
          this.done.push({
            id: e.id,
            name: e.name,
            checked: e.checked
          });
        else
          this.done.splice(this.done.indexOf(e), 1);
      },
      editTask: function (item) {
        this.editedTask = item;
      }
    }
  }
</script>