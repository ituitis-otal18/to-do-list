<template>
  <div id="app">
    <div class="row">
      <div class="mt-5 col-md-8 offset-md-2 text-center">
        <h2>My List:</h2>
        
        <div id="text-container">
          <hr>
          <input type="text" v-model="Text">
          <button @click="addTodo()" class="btn btn-primary ml-2">ADD</button>
          <hr>
        </div>
        
        <div id="list-container">
          <ToDoList @deleteData="deleteData($event)" v-for="todo in List" :key="todo.id" :data="todo"/>
        </div>

      </div>
    </div>
  </div>
</template>

<script>
  import ToDoList from './components/Container.vue'
  import axios from "axios"

  export default {
    name: 'app',
    components : {
      ToDoList
    },
    data(){
      return {
        Text : "",
        List : []
      }
    },
    methods : {
      addTodo(){
        axios.post("https://to-do-list-vue.firebaseio.com/List.json",{text : this.Text})
        .then(response => {
          console.log(response)
            let data = {
            text: this.Text,
            id: response.data.name
          }
          this.List.push(data)
        })
        .catch(e => {
          console.log(e)
        })
      },
      deleteData(id){
        console.log(id)
        axios.delete("https://to-do-list-vue.firebaseio.com/List/"+id+".json")
        .then(response => {
          console.log(response)
          for(let i=0; i<this.List.length; i++) if(id == this.List[i].id) this.List.splice(i,1)
        })
        .catch(e => {
          console.log(e)
        })
      }
    },
    created(){
      axios.get("https://to-do-list-vue.firebaseio.com/List.json")
      .then(response => {  
        for(let key in response.data){
          let data = {
            text: response.data[key].text,
            id: key
          }
          this.List.push(data)
          console.log(data)
        }
      })
      .catch(e => {
        console.log(e)
      })
    }
  }
</script>

<style>
  #app {
    font-family: Arial, Helvetica, sans-serif;
    color: white;
  }
  #text-container {
    display: none
  }
  hr {
    border: 1px dotted white;
  }
  .btn {
  font-size:12px;
}
</style>