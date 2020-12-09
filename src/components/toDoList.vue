<template>
  <v-container>
    <v-row class="text-center">
      <v-col cols="12" class="mb-6 projectTitle">
        {{ msg }}
      </v-col>

    </v-row>
    <div class="text-center">
      <input class="inputTask" type="text" name="something" placeholder="Enter Task" v-model="newTask"/>
        <v-btn style="margin-left:10px;" @click="add">
          <v-icon>
            mdi-plus
          </v-icon>
          Add
        </v-btn>
    </div>
    <br>
    <div class="list-tasks" v-for="(task,index) in array" :key="task.id">
        <div class="text-center">
            <input class="check" type="checkbox" v-model="task.completed" @click="completed(task)">
            <div  v-if="!task.editStatus" @click="editTask(task)" class="task-label" :class="{completed : task.completed}">
            {{task.title}} 
            </div>
            <input v-else class="task-edit" type="text" v-model="task.title" @blur="doneEdit(task)" @keyup.enter="doneEdit(task)" @keyup.esc="cancelEdit(task)">
        </div>
        
        <div class="remove-task" @click="removeTask(index)">
            &times;
        </div>

    </div>
    <br>
    <div v-if="showBtn()" class="completeBtn" @click="removeAllComp()">
        <button>Clear completed</button>
    </div>
  </v-container>
  
  
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";
@Component
export default class SampleComponent extends Vue {
  // Props
  @Prop({ default: "Hello World" }) msg: string;
  // Data
  count = 0;
  newTask = '';
  array = [];   
  editCache = '';
  // Computed
  get NextCount(): number {
    return this.count + 1;
  }
  // methods
  add() {
    
      if (this.newTask !== ''){ //check if task is empty or not
          this.array.push({
              id: this.count,
              title: this.newTask,
              show: true,
              completed: false,
              editStatus: false,
          })
          this.count++;
          this.newTask = '';
          
      }
  }
  removeTask(index){
      this.array.splice(index,1) //remove one item
  }

 //edit task
  editTask(task){
      task.editStatus = true
      this.editCache = task.title
  }

  doneEdit(task){
      if (task.title !== ''){
          task.editStatus = false
      }else{
          task.title = this.editCache
      }
  }

  cancelEdit(task){
      task.editStatus = false
      task.title = this.editCache
  }

  showBtn(){
      if ((this.array.filter(task => task.completed)).length>0){
          return true
      }
      
  }

removeAllComp(){
    this.array = this.array.filter(task => !task.completed)
}
  // lifecycle hooks
  created() {
    console.log("[SampleComponent.vue] created");
  }
  mounted() {
    console.log("[SampleComponent.vue] mounted");
  }
  updated() {
    console.log("[SampleComponent.vue] updated");
  }
  destroyed() {
    console.log("[SampleComponent.vue] destroyed");
  }
}
</script>
