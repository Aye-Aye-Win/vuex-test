<template>
      <div>
      <h1 class="text-center">All to do</h1>
            <div class="container">
                  <div class="row">         
                  <AddTodo/>
                  <FilterTodo/>
                  </div>
                  <div class="row">
                       <div class="col-md-4 my-4" v-for="todo in myTodos" :key="todo.id">
                            <b-card @dblclick="toggleCompleted(todo)"
                            :bg-variant="dynamicBackground(todo)" text-variant="white" class="text-center">
                            <b-card-text class="d-flex justify-content-between">
                               <span>{{todo.title}}</span>
                               <span @click="deleteTodo(todo.id)"><b-icon icon="trash-fill" variant="danger"></b-icon></span>
                            </b-card-text>
                            </b-card>
                        </div>
                  </div>
            </div>
      </div>
</template>

<script>
import { mapActions, mapGetters } from 'vuex'
import AddTodo from './AddTodo.vue'
import FilterTodo from "./FilterTodo.vue";

export default {
      components:{AddTodo,FilterTodo},
      computed:mapGetters(["myTodos"]),
      methods:{
            toggleCompleted(todo){
                  todo.completed = ! todo.completed;
                  this.updateTodo(todo);
            },
            dynamicBackground(todo){
              return todo.completed ? 'success' : 'primary'
            },
            ...mapActions(["getTodos","deleteTodo","updateTodo"])},
      mounted(){
            this.getTodos();
      }
}
</script>

<style>

</style>