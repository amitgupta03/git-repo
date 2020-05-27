<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      
    </v-app-bar>

    <v-content>
      <HelloWorld/>
      <TodoList/>
    </v-content>
  </v-app>
</template>

<script>
import HelloWorld from './components/HelloWorld';
import TodoList from './components/TodoList';

export default {
  name: 'App',

  components: {
    HelloWorld,
    TodoList
  },

  data: () => ({
    //
  }),
};
</script>
