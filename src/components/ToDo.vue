<template>
  <div class="container">
    <h1>Welcome to my todo</h1>

    <input type="text" v-model="task" placeholder="insert new task" v-on:keyup.enter="getTask()"/>
    <button @click="getTask()">add task</button>

    <div class="task" v-for="(toDo, i) in taskArr" :key="i" :class="isTaskCompleted(i) ? 'done' : ''">
      <div class="text-container">
        <h3>{{ toDo }}</h3>
      </div>

      <div class="buttons">
        <div>
          <button :class="isTaskCompleted(i) ? 'task-completed' : 'complete'" @click="completed(i)" >{{isTaskCompleted(i) ? 'undone' : 'completed'}}</button>
        </div>
        <div>
          <button class="delete" @click="deleteTask(i)">delete</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ToDo",

  data() {
    return {
      task: "",
      taskArr: [],
      selectedTasks: [],
    };
  },

  methods: {
    getTask() {
      this.taskArr.push(this.task);
      this.task= ""
    },

    completed(i) {
    
      if (this.isTaskCompleted(i)){
        let restoredTask = this.selectedTasks.findIndex((n)=> n === i);
        this.selectedTasks.splice(restoredTask,1);
      }else {
          this.selectedTasks.push(i);
      }
    },

    deleteTask(i) {
      this.taskArr.splice(i, 1);
    },

     isTaskCompleted(i) {
      
      let isSelected = this.selectedTasks.find((task) => task == i);

      return  (isSelected !== undefined ? true : false)
        
     },

  },
};
</script>

<style scoped >
.task {
  display: flex;
  justify-content: flex-end;
  border: 1px solid grey;
  margin: 20px auto;
  width: 500px;
}
button {
  padding: 10px 20px;
  border-radius: 15px;
}
.buttons {
  display: flex;
}
.text-container {
  min-width: 200px;
}
.complete {
  background-color: green;
}
.delete {
  background-color: red;
}
.done {
  background-color: grey;
}
.task-completed {
    background-color: grey;
}
</style>



