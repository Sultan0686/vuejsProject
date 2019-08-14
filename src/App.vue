<template>
  <div id="app">
    <!-- <div class="row">
      <div class="col s6">
        <myButton>Save</myButton>
      </div>
      <div class="col s6">
        <myButton>Delete</myButton>
      </div>
    </div> -->
    <div class="container">
      <todo></todo>
    </div>
    


  </div>
</template>

<script>
import myButton from './components/myButton'
import todo from './components/todo'

export default {
  name: 'app',
  components: {
    myButton,
    todo
  },
  data(){
    return{
      
    }
  }
  
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
