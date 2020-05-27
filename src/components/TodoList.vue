<template>
<div>
    <v-card max-width="700" class="mx-auto">
      <v-toolbar color="deep-purple accent-4"  dark >
        <v-toolbar-title>Todo List</v-toolbar-title>
        <v-spacer></v-spacer>
      </v-toolbar>
    <v-spacer></v-spacer>
     <v-text-field label="Enter Todo Item" filled v-model="newTodo" @keyup.enter="addTodo"></v-text-field>
  
      <v-list >
        <todo-item  v-for="(todo,index) in todosFiltered"  :key="todo.id" :todo="todo" :index="index" 
        @removedTodo="removeTodo" @finishedEdit="finishedEdit" >
            
             <!-- <v-checkbox  color="primary" v-model="todo.completed"></v-checkbox>
             <div v-if="!todo.editing" @dblclick="editTodo(todo)"  :class="{ completed : todo.completed }">{{todo.title}}</div>
             <v-text-field v-else  v-model="todo.title" @keyup.enter="doneEdit(todo)"  @blur="doneEdit(todo)" ></v-text-field>
         
          <v-list-item-icon>
            <v-icon @click="removeTodo(index)">x</v-icon> 
          </v-list-item-icon>  -->
        </todo-item>
      </v-list>
      <v-divider></v-divider>
        <v-footer>
    <v-spacer></v-spacer>
     <div style="float:left">{{ remaining }} items left</div>
  </v-footer>
  <div>
      <v-btn small   @click="filter='all'">All</v-btn>
      <v-btn small  @click="filter='active'">Active</v-btn>
      <v-btn small  @click="filter='completed'">completed</v-btn>

  </div>
   
    </v-card>
</div>
</template>
<script>

import TodoItem from './TodoItem'

  export default {
    name: 'todo-list',
    components :{
      TodoItem
    },
    data () {
        return{
            newTodo: '',
            idForTodo: 3,
            beforeEditCache: '',
             filter: 'all',
            todos: [
                {
                'id': 1,
                'title': 'first todo item',
                'completed': false,
                'editing': false,
                },
                {
                'id': 2,
                'title': 'second todo item',
                'completed': false,
                'editing': false,
                }
            ]
        }
    },
    computed: {
        remaining() {
          return this.todos.filter(todo => !todo.completed).length
        },
        todosFiltered() {
            if (this.filter == 'all') {
                return this.todos
            } else if (this.filter == 'active') {
                return this.todos.filter(todo => !todo.completed)
            } else if (this.filter == 'completed') {
                return this.todos.filter(todo => todo.completed)
            }
            return this.todos
         }
    },
    methods:{
        addTodo() {
            if (this.newTodo) {
                this.todos.push({
                    id: this.idForTodo,
                    title: this.newTodo,
                    completed: false,
                    editing: false,
                })
                this.newTodo = ''
                this.idForTodo++;
            }
        },
        removeTodo(index) {
             this.todos.splice(index, 1)
         },
         
        editTodo(todo) {
            this.beforeEditCache = todo.title
            todo.editing = true
        },
        doneEdit(todo) {
            if (todo.title.trim() == '') {
                todo.title = this.beforeEditCache
            }
            todo.editing = false
        },
        finishedEdit(data){
          this.todos.splice(data.index,1,data.todo)
        }
        
    }
  }
</script>
<style>
  .completed {
    text-decoration: line-through;
    color: grey;
  }
  
</style>
