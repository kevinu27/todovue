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
        <li   v-for="(task, index) in tasks" v-bind:key="index" :class="[task.greenColor ? 'greenColor' :'redColor']" >
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
      greenColor: null,
     


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
      // this.tasks= this.tasks.filter(task => task.index === index)
      this.tasks.splice(index, 1)
   },
  timerCheck: function () {
  let that = this;
  setInterval(function () { 

    for(let i = 0; i< that.tasks.length; i++){
      console.log("loopeando en el for")
      if(that.tasks[i].deathlineMonth >= new Date().getMonth() + 1){
          console.log("mismo mes o menos")
          that.tasks[i].monthValidation = true  }

      if(that.tasks[i].deathlineDay > new Date().getDate()){
          that.tasks[i].dayValidation = true
          console.log("condicion de pasado de fecha")
        }
        if(that.tasks[i].dayValidation && that.tasks[i].monthValidation){
          console.log("validacion de dia y mes pasada-------------")
          that.tasks[i].greenColor = true
             console.log("that.task[]", that.tasks)
        }  else {
           console.log("validacion de dia y mes NOOOO pasada-------------")
           that.tasks[i].greenColor = false    
           console.log("that.task[]", that.tasks)
        }
}// fin del bucle for

// mejorar la condicion, no esta bien hecha


      console.log("ejecucion del timer")
      // console.log("green", that.greenColor)
      // console.log("tasks", that.tasks)
      // console.log("date", new Date().getDate())
      // console.log("that.tasks[0].deathlineDay", that.tasks[0].deathlineDay)

    // }, 3600000);
       }, 3000);
   }
   
  },
  mounted () {
  this.timerCheck()
        }
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
    /* background-color: #42b983; */
margin-top: 15px;
border-radius: 5px;
}

.greenColor{

    background-color: #42b983;
}

.redColor{
    background-color: #b94242;

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
