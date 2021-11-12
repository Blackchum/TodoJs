<!-- Please remove this file from your project -->
<template>
  <center>
    <div id="app">
      <div class="container">
        <h1> To Do List </h1>
        <input
          class="input" 
          v-model="newToDo"
        />
        <button class="add-button" v-on:click="add()">Add</button>
        <ul style="List-style-type: none;">
          <li v-for="(todo,i) in existingToDo" :key="i">
            <div v-if="!existingToDo[i].edit">
                {{ i + 1}}: {{todo.text}}
              <button class="add-button" v-on:click="edit(i)">Edit</button>
              <button class="add-button" v-on:click="remove(i)">X</button>
            </div>
            <div v-else-if="existingToDo[i].edit">
              <input type="text" v-model="existingToDo[i].newValue">
              <button class="add-button" v-on:click="save(i)">save</button>
              <button class="add-button" v-on:click="edit(i)">cancel</button>
            </div>
          </li>
        </ul>
      </div>
    </div>
  </center>
</template>

<script>
  export default{
    name: 'app',
    data() {
      return{
        newToDo:'',
        existingToDo:[]
      }
    },

    methods:{
      add(){
        this.existingToDo.push({
          text: this.newToDo,
          edit: false,
          newValue: this.newToDo,
          id: new Date().valueOf()
        }),
        this.newToDo = ''
      },

      save(i){
        this.existingToDo[i].text = this.existingToDo[i].newValue;
        this.edit(i);
      },
      
      edit(i){
        this.existingToDo[i].edit = !this.existingToDo[i].edit;
      },

      remove(i){
        this.existingToDo.splice(i, 1)
      },
    }
  }
</script>



<style> 
</style>


