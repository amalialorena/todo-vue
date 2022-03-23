<template>
  <div class="container">
    <h1>Welcome to my todo</h1>

    <input type="text" v-model="inputTask" placeholder="insert new task" v-on:keyup.enter="createTask()"/>
    <button @click="createTask()">add task</button>

    <div class="task" v-for="(toDo, i) in taskArr" :key="i">
      <div class="text-container">
        <h3>{{ toDo.text }}</h3> <h3>{{ toDo.isCompleted }}</h3>
      </div>

      <div class="buttons">
        <div>
          <button @click="toggleCompleted(toDo.id)" >{{isTaskCompleted(toDo.id) ? 'undone' : 'completed'}}</button>
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
      inputTask: "",
      taskArr: [],
      selectedTasks: [],
    };
  },

  methods: {
    createTask() {
     
      const newTask = {
        id: Math.random() *1000,
        text: this.inputTask,
        isCompleted : false
      };
      
      this.taskArr.push(newTask);
      this.inputTask= "";
    },

    toggleCompleted(id) {

    this.selectedTasks = this.taskArr.filter((t)=> t.id == id);
    
    for(let i = 0; i< this.selectedTasks.length; i++) {
      
      if(this.selectedTasks[i].isCompleted){
        this.selectedTasks[i].isCompleted = false
        
      } else {
        this.selectedTasks[i].isCompleted = true
       
      }
    }
    
    },

    deleteTask(i) {
      this.taskArr.splice(i, 1);
    },


     isTaskCompleted(id) {
     
           for(let i = 0; i < this.taskArr.length; i++) {
             if (this.taskArr[i].id == id) {
               console.log(this.taskArr[i].isCompleted,this.taskArr[i].text)
               return this.taskArr[i].isCompleted
             }
           }
        
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



