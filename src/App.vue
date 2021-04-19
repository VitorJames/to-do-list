<template>
  <v-app>
    <Header/>
    <v-main class="grey lighten-3 px-0">
      <ToDoList/>
    </v-main>
  </v-app>
</template>

<script>
import Header from './components/Header';
import ToDoList from './components/ToDoList';

export default {
  name: 'App',

  components: {
    Header,
    ToDoList,
  },

  data: () => ({
    //
  }),
};
</script>
