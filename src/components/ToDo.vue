<template>
  <div class="container">
    <h1>Welcome to my todo</h1>
    
      <input type="text" v-model="task" placeholder="task" />
      <button @click="getTask()">submit</button>
      <!-- <input type="submit" @click="submit()"/> -->
    
    <div class="task">
        <div class="text-container">
            <h3></h3>
            
        </div>
      
      <div class="buttons">
        <div>
          <button class="completed">completed</button>
        </div>
        <div>
          <button class="delete">delete</button>
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
    };
  },

  methods: {
      getTask(){
       this.taskArr.push(this.task);
        console.log(this.taskArr)
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
  min-width: 400px;
  
}
button {
  padding: 10px 20px;
  border-radius: 15px;
}
.buttons {
    display: flex;
}
.text-container{
    min-width: 200px;
}
.completed {
  background-color: green;
}
.delete {
  background-color: red;
}
</style>