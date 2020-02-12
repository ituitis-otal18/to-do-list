<template>
  <div class="container">
    <table class="mt-5 col-md-8 offset-md-2 text-center element">
      <tr>
        <th><a class="element pl-3 mt-2 md-2">{{ data.text }}</a></th>
        <th class="element2"><button @click="$emit('deleteData', data.id)" class="btn btn-primary delete">DELETE</button></th>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  name: 'ToDoList',
  props: ["data"]
}
</script>

<style>
.element {
  background-color: white;
  color: black;
  float: left;
}
.element2 {
  display: block;
  float: right;
}
.delete {
  background-color: red;
  display: none;
  float: right;
}
.delete:hover {
  background-color: darkred;
}
</style>
