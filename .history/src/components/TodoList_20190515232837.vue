<template>
  <div>
    <div>
      <h1>TodoList</h1>
    </div>
    <div v-for="task in tasks" :key="task.doTask"></div>
    <div>
      <label for>
        タスク
        <input v-model="newTaskName">
      </label>
      <button @click="addTask(baseUrl)">add</button>
    </div>
    <div class="task-list">
      <div class="done">
        <h2>完了</h2>
        <div v-for="(task,a) in tasks" :key="`first${task.id}`" v-if="task.taskFinish">
          <div class="name">タスク: {{task.doTask}}</div>
          <button @click="task.taskFinish= false">未完へ</button>
          <button @click="deleteTask(a)">削除</button>
        </div>
      </div>

      
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "TodoList",
  data() {
    let list = new Array();
    const axious = require("axios");
    return {
      id: 0,
      newTaskName: "",
      isTaskDone: false,
      tasks: list,
      item: { id: this.id, doTask: this.newTaskName, taskFinish: false },
      baseUrl: "https://to-hutohu.trap.show/naro-todo-server/hosshii/tasks"
    };
  },
  methods: {
    addTask(url) {
      if (this.newTaskName !== "") {
        this.id++;
        this.item = {
          id: this.id,
          doTask: this.newTaskName,
          taskFinish: false
        };
        this.tasks.push(this.item);

        this.newTaskName = "";
        axios
          .post(url, this.item)
          .then(console.log(this.id), console.log(this.tasks[this.id-1]));

        //console.log(this.tasks[this.tasks.length - 1].id);

        //console.log(this.id);
      }
    },
    deleteTask(arrayIndex) {
      this.tasks.splice(arrayIndex, 1);
      //console.log(arrayIndex)
      //axios.delete(this.baseUrl+"/"+arrayIndex);
    },
    getTask(url) {
      axios
        .get(url)
        .then(response => {
          // handle success
          if (this.tasks.length !== 0) {
            this.tasks = response.data;
            this.id = this.tasks[this.tasks.length - 1].id;
          }
          console.log(this.tasks[this.tasks.length - 1].id);
        })
        .catch(function(error) {
          // handle error
          console.log(error);
        })
        .finally(function() {
          // always executed
        });
    }
  },
  mounted() {
    this.$nextTick(this.getTask(this.baseUrl));
  },
  computed: {}
};
</script>

<style >
</style>