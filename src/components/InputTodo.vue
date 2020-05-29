<template>
    <div>
          <v-text-field label="Enter Todo Item" filled :value="value"
      @input="customNewTodo($event)"  @keyup.enter="addTodo"></v-text-field> 
    </div>
</template>

<script>
export default {                    
    name : "input-todo",
    props: {
        value: {
            type: String,
            default: '',
            },
    },
    data(){
        return{
           val:''
        }
    },
    
    methods:{
        customNewTodo(val){
            this.$emit('input',val);
        },
         addTodo() {
            this.$emit('addedTodo',this.val)
        },
       
    }
}
</script>
