<template>
 <h1>to do app</h1>
 
<div class="form">
<div >
<p v-if="red" class="redd">enter an task</p>
 <label>Task :  </label>
 <input type="text"   v-model="task" @keyup.enter="add" >
</div>
<div class="b" v-if="todos.length">

<div class="m">
<label for="all">mark all</label>
<input type="checkbox" name="markall" id="all" @click="markAll"  v-model="doneAll">
</div>
<button  id="delete" @click="deleteAll">delete All</button>
</div>


<div class="buttons">
</div>
<button type="submit"  @click="add" class="adding" >submit task</button>

</div>
 
 

 <ul >
 <li v-for="(todo,index) in todos" :key="todo.id" >
 <h3 :class="{mark:todo.status}" @click="cancel(todo)"> {{todo.content}} </h3>
 <p @click="delete_task(index)" class="delete">delete</p>
  </li>
 
 </ul>
 
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import {ref} from 'vue'

export default {
  name: 'App',
  setup() {
  const task= ref('')
  const todos=ref([])
  let red=ref(false)
  const doneAll= ref('')
  function add(){
    
    if(task.value==' '){
      red.value=true
    
      task.value=' '

    }
    
    else{
         if(red.value==true){
           red.value=false
         }
         if(todos.value.includes(task.value)==false){

           todos.value.push({
             id:Date.now(),
             content:task.value,
             status:false
             
           })
         
         }
         else{
           console.log ("task already exists")
         }

        // console.log(show)

    }
    
      task.value=' '
     
  }
 

  function cancel(todo){
    console.log(todo.status)
   return todo.status=!todo.status

      
  } 
  function delete_task(index){
   todos.value.splice(index,1)
  }
  function markAll(){
    // console.log(!doneAll.value)
    if(!doneAll.value){
         
          todos.value.forEach((todo)=>{
                 todo.status=true
          })
    }
    else{
       todos.value.forEach((todo)=>{
                 todo.status=false
          })
    }
  }
  function deleteAll(){
    let confirmation= confirm(" are you sure you want to delete all")

    if(confirmation==true){
      todos.value=[]
    }

  }
 console.log(red)
  return {
    task,add,todos,cancel,delete_task,red,markAll,doneAll,deleteAll
  }
  }

}
</script>

<style>
*{
  font-family:"poppins";
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
li{
  list-style-type: none;
  
  display:flex;
  margin-bottom: 15px;
  background: rgb(206, 204, 204);
  padding:5px;
  border-radius: 10px;
  justify-content: space-around;
  
}
.form{
display:flex;
flex-direction: column;
}
.delete{
  background:rgb(238, 67, 67);
  color:black;
  font-weight:600;
  border: none;
  width: 90px;
  font-size: 18px;
  padding:18px;
  text-align: center;
  border-radius: 15px;
  cursor: pointer;
}

.mark{
  text-decoration: line-through;
}
input[type="text"]{
  width:70%;
  height: 29px;
}
.adding{

  width:50%;
  margin:auto;
  background:rgb(21, 219, 64);
  border: none;
  margin-top: 15px;
  padding: 10px;
  font-size: 17px;
  font-weight: 500;
  transition: .4s all ease-in-out;
}
.adding:hover{
  color:white;
}
h1{
  text-transform: capitalize;
}
.redd{
  color: red;
  font-size:19px;
}
.b>button{
 border: none;
 background: rgb(250, 34, 34);
 padding:9px;
 color: white;
}
.b{
  display:flex;
  flex-direction: row;
  gap: 30px;
  justify-content: center;
  align-items: center;
  margin: 40px;
}
.m{
display: flex;
flex-direction:column;

}














</style>
