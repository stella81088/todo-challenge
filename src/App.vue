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
    margin-top:-24px;
    margin-left: 50px;
  }
  .task-edit{
    display:flex;
    margin-top:-23px;
    margin-left:55px;
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
    cursor:pointer;
    margin-right:10px;
  }
  .not-fav-task{
    cursor: pointer;
    flex-grow: 1;

    margin-top:-25px;
    margin-left:24px;
  }
  .fav-task{
    cursor: pointer;
    flex-grow: 1;
    margin-top:-25px;
    margin-left:24px;
    color: black;
  }


  .heading{
    margin-top:5px;
    margin-bottom: 5px;
  }  

  .headingBtn{
    margin-left:5px;
    margin-right:5px;
    background-color: white;
    padding: 2px;
    border-radius: 5px;
  }

  .active{
    background-color: lightcyan;
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

  .fade-enter-active .fade-leave-active {
    transition: opacity 1s;
  }

  .fade-enter, .fade-leave-to {
    opacity:0;
  }
</style>
