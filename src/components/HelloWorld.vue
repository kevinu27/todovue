<template>
<div class="main">
  <div class="hello">
    <h1>{{ msg }}</h1>
    <div class="addTask">
      <label for=""> Task Name</label>
    <input type="text" v-model="taskName" >
</div>
          <button @click="addTask">Add Task</button>
  </div>
     <div class="task">
        <li v-for="(task, index) in tasks" v-bind:key="task" >{{task.name}} - {{task.date}} {{index}} </li>
      </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      tasks:[{
         name: "",
         date: new Date().getMonth() + 1}
      ],
      taskName: '',
      // task: {
      //   name: "",
      //    date: new Date().getMonth() + 1
      // }
    }

 },  
 methods: {
    addTask() {
    console.log("-----")
    // console.log("task",this.task)
    // const tasknameAfter = this.task
    this.tasks.push({
      name: this.taskName,
      date: new Date().getMonth() + 1
    })
    // console.log("tasks", this.tasks)
    // this.taskName = ''
    //  console.log("-----")
    },
  },
  }
</script>

<style scoped>
.main{display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;}

button{
padding: 10px;
padding-left: 20px;
padding-right: 20px;
margin-bottom: 30px;
}
.addTask{
  display: flex;
 
  justify-content: center;
}
label{
  font-weight: bold;
  margin-right: 30px;
}
.task{

  width: 70%;
  margin-top: 30px;
  font-weight: bold;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.task li{
  width: 70%;
  padding: 40px;
    background-color: #42b983;
margin-top: 15px;
border-radius: 5px;
}

input{
  margin-bottom: 20px;
  width: 30%;
  height: 20px;
}

.hello{
background-color: rgb(240,240,240);
border-radius: 10px;
box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px;
width: 60%;
}

h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
