<template>
<div class="main">
  <div class="hello">
    <h1>{{ msg }}</h1>
    <div class="addTask">
      <label for=""> Task Name</label>
    <input type="text" v-model="taskName" >
     <label for=""> Due to</label>
    <input type="date" v-model="dueDate">
</div>
          <button @click="addTask">Add Task</button>
  </div>
     <div class="task" v-if="!emptiness > 0">
        <li v-for="(task, index) in tasks" v-bind:key="index" >
        <div class="taskDiv">
          <div class="closingX"> <h3 @click="removeTask(index)">X</h3> </div>
          <div>
        <h2>{{task.name}}</h2></div> 
        <div>
        due TIme:{{task.deathlineDay}}/{{task.deathlineMonth}} </div> 
        <div> Creation date {{task.CreationDay}}/{{task.CreationMonth}}</div></div> </li>
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
      tasks:[
      ],
      taskName: '',
      dueDate:"",
      emptiness: true,

    }

 },  
 methods: {
    addTask() {
    this.tasks.push({
      name: this.taskName,
      date: new Date().getMonth() + 1,
      deathlineMonth: parseInt(this.dueDate.substring(5, 7)),
      deathlineDay: parseInt(this.dueDate.substring(8,10)),
      CreationMonth: new Date().getMonth() + 1,
      CreationDay: new Date().getDate()
      
    })
    console.log("deathline", new Date())
     console.log("tasks", this.tasks)
    this.emptiness = false
    },
   removeTask(index){
// this.tasks.filter(task => task.index !== index)
this.tasks.splice(index, 1)
console.log("index", index)
   } 
  },
  }
</script>

<style scoped>
.closingX h3{
    margin-top: 15px;
    padding-top: 0;


   
}
.closingX{
  display: flex;
  justify-content: flex-end;
    width: 100%;

}

h2 {
  margin-top: 0px;
}
.taskDiv{
  display: flex;
  flex-direction: column;
  align-items: center;
}
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
  margin-right: 15px;
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
  padding: 30px;
  padding-top: 0;
    background-color: #42b983;
margin-top: 15px;
border-radius: 5px;
}

input{
  margin-bottom: 20px;
  width: 30%;
  height: 20px;
  margin-right: 3%;
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
