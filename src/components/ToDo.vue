<template>
  <div class="container">
    <nav>
      <img src="src/assets/img/myToDoLogo.svg" alt="" />
    </nav>
    <main>
      <!-- <div class="title">
        <img src="src/assets/img/tasksIcon.svg" alt="" />
        <h2>Tasks</h2>
      </div> -->
      <div class="input-container">
        <input
          type="text"
          v-model="inputTask"
          placeholder="Add a task"
          v-on:keyup.enter="createTask()"
        />

        <button class="add-task-btn" @click="createTask()">
          <img src="src/assets/img/addTask.svg" alt="" />
        </button>
      </div>
      <div class="task-count">Remaining tasks: {{ taskArr.length }}</div>

      <div class="task" v-for="(toDo, i) in taskArr" :key="i">
        <div class="todo-container">
          <div class="button">
            <button
              @click="toggleCompleted(toDo.id)"
            >
              <img :src="isTaskCompleted(toDo.id) ? 'src/assets/img/taskCompleted.svg' : 'src/assets/img/completeTask.svg'" alt="" />
            </button>
          </div>

          <div class="text-container">
            <h3 :class="isTaskCompleted(toDo.id) ? 'completed-task' : ''">
              {{ toDo.text }}
            </h3>
          </div>
        </div>

        <div class="button, delete">
          <button @click="deleteTask(i)">
            <img src="src/assets/img/trash.svg" alt="" />
          </button>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
function ciao() {
  return "string";
}
const ciao1 = () => {
  return "string";
};

const ciao2 = (param) => "string";

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
      if (this.inputTask != "") {
        const newTask = {
          id: Math.random() * 1000,
          text: this.inputTask,
          isCompleted: false,
        };
        this.taskArr.push(newTask);
      }

      this.inputTask = "";
    },

    toggleCompleted(id) {
      const selected = this.taskArr.map((t) => {
        if (t.id === id) {
          t.isCompleted = !t.isCompleted;
        }
      });
    },

    deleteTask(i) {
      this.taskArr.splice(i, 1);
    },

    isTaskCompleted(id) {
      for (let i = 0; i < this.taskArr.length; i++) {
        if (this.taskArr[i].id == id) {
          return this.taskArr[i].isCompleted;
        }
      }
    },
  },
};
</script>

<style scoped lang="scss">
.container {
  background-color: #100f13;
  color: white;
  min-height: 100vh;
  overflow: auto;
}

nav {
  height: 70px;
  background-color: #191920;
  display: flex;
  align-items: center;
  border-bottom: 2px solid #474849;
  padding-left: 10px;
}

main {
  max-width: 700px;
  margin: 0 auto;
  padding: 0 10px
  ;
}

.title {
  margin-top: 120px;
  margin-bottom: 80px;
  display: flex;
  h2 {
    margin-left: 20px;
    font-size: 35px;
  }
}

::placeholder {
  color: white;
  font-size: 18px;
}

input {
  width: 100%;
  height: 50px;
  border-radius: 8px;
  background-color: #131318;
  border: 3px solid #16161c;
  padding-left: 60px;
  color: white;
  font-size: 20px;
}

.input-container {
  position: relative;
  margin-top: 100PX;;
}

button {
  all: unset;
  height: 40px;
  cursor: pointer;
}

.add-task-btn {
  position: absolute;
  top: 5px;
  left: 5px;
}

.task {
  position: relative;
  display: flex;
  justify-content: space-between;
  margin: auto;
  width: 100%;
  background: #191920;
  border-radius: 8px;
  margin-bottom: 18px;
  h3 {
     font-size: 20px;
  } 
  transition: all 2s;
}

.task-count {
  margin-top: 30px;
  margin-bottom: 30px;
  margin-left: 10px;
  font-weight: bold;
  font-size: 20px;
}

.text-container {
  width: 100%;
  h3 {
    margin-left: 10px;
  }
}

.todo-container {
  display: flex;
  align-items: center;
  margin-left: 10px; 
}

.delete {
  align-self: center;
  margin-right: 10px;
  height: 40px;
  position: absolute;
  top: auto;
  right: 0;
  display: none; 
}

.button {
  height: 40px;
}

.task:hover {
  .delete {
    display: block;
  }
}

.completed-task {
  text-decoration: line-through;
}
</style>



