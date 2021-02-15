<template>
   <div class="container">
     <h1>Todo List</h1>
     <!-- Adds new todo item to the list if not editing an existing item -->
     <div v-if="!isEditing">
       <input type="text" v-model="todo">
       <input class="btn-add" type="submit" value="Add" v-on:click="store">
     </div>
     <!-- Calls the update method if editing the todo item -->
     <div v-else>
       <input  type="text" v-model="todo">
       <input class="btn-update" type="submit" value="Update" v-on:click="update">
     </div>
     <!-- Displays the todo items -->
       <div class="list" v-for="(todo,index) in todos" :key="todo">
         {{todo}}
         <div class="buttons">
           <button class="btn-edit" v-on:click="edit(index,todo)">Edit</button>
           <button class="btn-remove" v-on:click="remove(index)">Remove</button>
         </div>
       </div>
    
   </div>
</template>

<script>

export default {
    name:"App",
    components:{

    },
    data() {
     return{
       todo:"",
       todos: ['Go to work', 'Buy food'],
       isEditing: false,
       indexSelected: null
       }
      
    },
    
    methods:{
      //Adds new todo item to the todos array
      store(){
        this.todos.push(this.todo)
        this.todo = ""
      },
      //Edits the existing todo item
      edit(index,todo)
      {
        this.todo=todo
        this.indexSelected = index
        this.isEditing = true
      },
      //Updates the todo item in the todos array
      update()
      {
        this.todos.splice(this.indexSelected,1,this.todo)
        this.isEditing = false
        this.todo=""
      },
      //Removes todo item from the todos array
      remove(index)
      {
        this.todos.splice(index,1)
        
      }
    }
  
}
</script>

<style lang="scss">
 $font-stack: Helvetica, sans-serif;

 %btn{
   display: inline-block;
   border-radius: 5px ;
   padding: 8px 20px;
   margin:3px;
   color: #fff;

   &:hover{
     transform: scale(0.97);
   }
 }

 .btn-add{
   @extend %btn;
   background-color: #90369e ;
  
   
 }

 .btn-remove{
   @extend %btn;
   background-color: #d42815;
 }

 .btn-update{
   @extend %btn;
   background-color: #de910d;
 }
 
 .btn-edit{
   @extend %btn;
   background-color: #099114;
 }

 .container{
   width: 700px;
   margin: auto;
   height: 1000px;
   overflow: auto;
   font: 100% $font-stack;
   box-sizing: border-box;
   
  
  h1{
    text-align: center;
    background-color: #190638;
    color: #e0de81;
    border-radius: 10px;
  }

   .list{
     display: flex;
     justify-content: space-between;
     font-weight: bold;
     align-items: center;
     padding: 4px;
     border: 1px solid black;
     max-width: 100%;
     background-color: #d6d1c7;
     margin: 5px;
     list-style-type: none;
     box-shadow: 5px;
   }

   input[type=text]{
       width: 80%;
       padding: 12px 20px;
       margin: 8px 6px;
       display: inline-block;
       border: 1px solid #ccc;
       border-radius: 4px;
       box-sizing: border-box;
   }
   
 }
</style>
