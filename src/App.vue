<template>
  <v-app>
    <v-main>
      <SampleComponent msg="TODO: Create a todo list"/>
    </v-main>
  </v-app>
</template>

<script lang="ts">
import Vue from 'vue';
import SampleComponent from './components/toDoList.vue';

export default Vue.extend({
  name: 'App',

  components: {
    SampleComponent,
  },

  data: () => ({
    //
  }),
});
</script>

<style>
#app{
  background-color:lightblue;
}
  .projectTitle{
    font-size: 36px;
  }
  .inputTask{
    display:relative;
    border: 2px;
    width:50%;
    height:50px;
    text-align: center;
    background-color:white;
    border-radius: 5px;

  }
  .check{
    margin-right: 40px;
    margin-top:5px;
  }
  .task-label{
    margin-top: -25px;
    margin-left: 40px;
  }
  .list-tasks{
    display: flex;
    background-color: white;
    justify-content: space-between;
    margin-bottom: 5px;
    padding-left: 5px;
    margin-left: 290px;
    width: 50%;
    border-radius: 5px;
  }

  .list-tasks:hover{
    background-color:beige;
  }

  .remove-task{
    margin-right:10px;
  }

  .task-edit{
    width: 150%;
    display:relative;

  }

  .completed{
    color: gray;
    text-decoration: line-through;

  }

  .completeBtn{
    background-color: white;
    display: block;
    text-align: center;
    border-radius: 5px;
    float:right;
    width: 200px;
  }
</style>
