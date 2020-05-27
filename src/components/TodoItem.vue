<template>
    <div>
        <v-list-item>
          <v-checkbox  color="primary" v-model="completed" @change="doneEdit"></v-checkbox>
             <div v-if="!editing" @dblclick="editTodo()"  :class="{ completed : completed }">{{title}}</div>
             <v-text-field v-else  v-model="title" @keyup.enter="doneEdit()"  @blur="doneEdit()" ></v-text-field>
         
          <v-list-item-icon>
            <v-icon @click="removeTodo(index)">x</v-icon> 
          </v-list-item-icon> 
        </v-list-item>
    </div>
</template>

<script>
export default {
    name : "todo-item",
    props : {
        todo:{type:Object,required:true},
        index:{type:Number,required:true}
    },
    data(){
        return{
            'id':this.todo.id,
            'title':this.todo.title,
            'completed':this.todo.completed,
            'editing':this.todo.editing,
            'beforeEditCache':'',


        }
    },
    methods:{
        removeTodo(index){
            this.$emit('removedTodo',index);
        },
        editTodo() {
            this.beforeEditCache = this.title
            this.editing = true
        },
         doneEdit() {
            if (this.title.trim() == '') {
                this.title = this.beforeEditCache
            }
            this.editing = false
             this.$emit('finishedEdit',{
                index:this.index,
                todo:{
                    'id':this.id,
                    'title':this.title,
                    'completed':this.completed,
                    'editing':this.editing,
                }
            })
        }
    }
    
}
</script>
