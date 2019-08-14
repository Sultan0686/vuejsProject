<template>
  <div>
      <h3>To-Do</h3>
    <div class="input-field" id="myDiv">
      <div class="row">
        <div class="col s12">
          <input
            id="todo"
            type="text"
            class="validate"
            autocomplete="off"
            v-model="todoInput"
            @input="inputValue"
          />
          <label for="todo">Enter new To-Do</label>
        </div>
      </div>
      <div class="row">
        <div class="col s6">
          <input type="date" id="deadline" autocomplete="off" v-model="pickDate" />
          <label for="deadLine">Choose deadline</label>
        </div>
        <div class="col s6">
          <label>
            <input type="checkbox" v-model="Important" />
            <span>Important</span>
          </label>
        </div>
      </div>
      <button
        class="btn waves-effect"
        v-on:click="addTask"
        :disabled="todoInput==='' || todoInput===null || pickDate ===null || pickDate ===''"
      >Save</button>
      <br />
      <br />
    </div>
    <br />
    <div class="container">
        <div class="row">
          <div class="col s6">
              <button class="btn waves-effect" :disabled="added===false" @click="filterByDate">Sort by date</button>
          </div>
          <div class="col s6">
              <button class="btn waves-effect" :disabled="added===false" @click="filterByImportance">Sort by importance</button>
          </div>
      </div>
      <div
        class="row row1"
        v-for="(task,index) in tasks"
        v-bind:key="index"
        v-bind:class="[{'row2':task.important}, {'row3':task.isEditing}]"
      >
        <div class="col s4">
          <p class="listText">{{task.list}}</p>
        </div>
        <div class="col s4">
          <p class="listText">Deadline: {{task.date}}</p>
        </div>
        <div class="col s4">
          <button
            class="waves-effect btn-floating btn"
            id="delete_btn"
            v-on:click="deleteList(index)"
          >
            <i class="material-icons">delete</i>
          </button>
          <button class="waves-effect btn-floating btn" id="edit_btn" v-on:click="editList(index)">
            <i class="material-icons">edit</i>
          </button>
        </div>
      </div>
      
    </div>
  </div>
</template>
<script>
import _ from "lodash"
export default {
  data() {
    return {
      todoInput: "",
      pickDate: "",
      tasks: [],
      index: 0,
      Important: false,
      isEditing: false,
      isEdit: false,
      added:false,
      oreder:"",
      oreder1:"",
    };
  },
  methods: {
    addTask() {
      this.added = true;
      if (this.isEdit) {
        this.tasks[this.index] = {
          list: this.todoInput,
          date: this.pickDate,
          important: this.Important,
        };
      } else {
        this.tasks.push({
          list: this.todoInput,
          date: this.pickDate,
          important: this.Important,
          isEditing: this.isEditing
        });
      }
      this.todoInput = "";
      this.pickDate = "";
      this.Important = false;
      this.isEdit = false;
    },
  
    editList(index) {
      this.isEdit = true;
      this.index = index;
      this.tasks[index].isEditing = true;
      this.todoInput = this.tasks[index].list;
      this.pickDate = this.tasks[index].date;
      this.Important = this.tasks[index].important;
    },
    deleteList(index) {
      this.tasks.splice(index, 1);
      this.todoInput = "";
      this.pickDate = "";
      this.Important = false;
      if(this.tasks.length === 0){
          this.added = false;
      }else{
          this.added = true;
      }

    },
      filterByDate(){
        if(this.oreder===""){
            this.tasks = _.orderBy(this.tasks, ["date"], ["esc"]);
            this.oreder = "esc";
        }else if(this.oreder==="esc"){
            this.tasks = _.orderBy(this.tasks, ["date"], ["desc"]);
            this.oreder = "desc";
        }else if(this.oreder==="desc"){
            this.tasks = _.orderBy(this.tasks, ["date"], ["esc"]);
            this.oreder = "esc";
        }
    },
    filterByImportance(){
      //  return this.tasks.filter(task =>{
      //      return task.important === true;
      //   })
        if(this.oreder1===""){
            this.tasks = _.orderBy(this.tasks, ["important"], ["esc"]);
            this.oreder1 = "esc";
        }else if(this.oreder1==="esc"){
            this.tasks = _.orderBy(this.tasks, ["important"], ["desc"]);
            this.oreder1 = "desc";
        }else if(this.oreder1==="desc"){
            this.tasks = _.orderBy(this.tasks, ["important"], ["esc"]);
            this.oreder1 = "esc";
        }
    },
    inputValue(event) {
      this.todoInput = event.target.value.toUpperCase();
    }
  },
  mounted: function() {
    document.addEventListener("DOMContentLoaded", function() {
      var elems = document.querySelectorAll(".datepicker");
      M.Datepicker.init(elems, {});
    });
  }
};
</script>
<style>
#myDiv {
  width: 400px;
  margin: auto;
}
#myDiv1 {
  text-align: left;
}
.listDiv {
  height: 50px;
  margin-bottom: 5px;
  background-color: antiquewhite;
}
.listText {
  text-align: left;
  font-size: 20px;
  line-height: 40px;
  font-family: "Handlee", cursive;
  font-weight: bold;
  margin: 0;
}
#delete_btn {
  background-color: rgb(194, 49, 49);
  vertical-align: top;
  margin-right: 15px;
}

.row1 {
  background-color: antiquewhite;
  padding: 8px;
  border-radius: 5px;
}
.row2 {
  background-color: rgb(236, 143, 22);
  padding: 8px;
  border-radius: 5px;
}
.row3 {
  background-color: rgb(131, 255, 137);
  padding: 8px;
  border-radius: 5px;
}
</style>

