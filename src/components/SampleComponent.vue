<template>
  <v-container>
    <v-row class="text-center">
      <v-col cols="12" class="mb-6 projectTitle">
        {{ msg }}
      </v-col>
    </v-row>

    <div class="text-center">
      <input
        class="inputTask"
        type="text"
        placeholder="Enter Task"
        v-model=newTask
        @keyup.enter="add"
      />

      <v-btn style="margin-left: 10px" @click="add">
        <v-icon> mdi-plus </v-icon>
        Add
      </v-btn>
    </div>
    <!-- heading -->

    <div class="text-center heading">
      <label
        ><input type="checkbox" :checked="!isTask()" @change="checkAll()" />
        Check All</label
      >
      <div>{{ remainingTasks }} task(s) left</div>
      <div>
        <button
          class="headingBtn"
          :class="{ active: filter == 'all' }"
          @click="filter = 'all'"
        >
          All Tasks
        </button>
        <button
          class="headingBtn"
          :class="{ active: filter == 'completed' }"
          @click="filter = 'completed'"
        >
          Completed Tasks
        </button>
        <button
          class="headingBtn"
          :class="{ active: filter == 'remain' }"
          @click="filter = 'remain'"
        >
          Active Tasks
        </button>
        <button
          class="headingBtn"
          :class="{ active: filter == 'fav' }"
          @click="filter = 'fav'"
        >
          Important
        </button>
      </div>
    </div>

    <!-- filtering the tasks -->
    <div class="list-tasks" v-for="(task, index) in filtered()" :key="task.id">
      <div class="keep-same">
        <input class="check" type="checkbox" v-model="task.completed" />

        <!-- <div class="fav-task" @click="favTask(task)">&star;</div> -->
        <div class="not-fav-task" @click="favTask(task)" v-if="!task.fav">
          &star;
        </div>
        <div class="fav-task" @click="favTask(task)" v-else>
          &#9733;
        </div>
        <div
          v-if="!task.editStatus"
          @click="editTask(task)"
          class="task-label"
          :class="{ completed: task.completed }"
        >
          {{ task.title }}
        </div>
        <input
          v-else
          class="task-edit"
          type="text"
          v-model="task.title"
          @blur="doneEdit(task)"
          @keyup.enter="doneEdit(task)"
          @keyup.esc="cancelEdit(task)"
        />
      </div>

      <div class="remove-task" @click="removeTask(index)">&times;</div>
    </div>
    <br />

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
  checked = false;
  newTask = "";
  array = [];
  editCache = "";
  filter = "all";
  // index = 0;

  // Computed
  get NextCount(): number {
    return this.count + 1;
  }
  get remainingTasks(): number {
    return this.array.filter((task) => !task.completed).length;
  }

  filtered() {
    if (this.filter == "all") {
      return this.array;
    } else if (this.filter == "completed") {
      return this.array.filter((task) => task.completed);
    } else if (this.filter == "remain") {
      return this.array.filter((task) => !task.completed);
    } else if (this.filter == "fav") {
      return this.array.filter((task) => task.fav);
    }
  }
  // methods
  add() {
    //check if task is empty or not
    //console.log(isFinite(this.newTask));
    if (this.newTask !== "") {
        this.array.push({
          id: this.count,
          title: this.newTask,
          show: true,
          completed: false,
          editStatus: false,
          fav: false,
        });
        this.count++;
        this.newTask = "";
      
    }
  }
  removeTask(index) {
    this.array.splice(index, 1); //remove one item
  }

  //edit task
  editTask(task) {
    task.editStatus = true;
    this.editCache = task.title;
  }

  doneEdit(task) {
    if (task.title !== "") {
      task.editStatus = false;
    } else {
      task.title = this.editCache;
    }
  }

  cancelEdit(task) {
    task.editStatus = false;
    task.title = this.editCache;
  }

  showBtn() {
    //clear completed btn
    if (this.array.filter((task) => task.completed).length > 0) {
      return true;
    }
  }

  favTask(task) {
    if (task.fav == false) {
      task.fav = true;
    } else {
      task.fav = false;
    }
  }
  removeAllComp() {
    //remove all the completed ones
    this.array = this.array.filter((task) => !task.completed);
  }

  isTask() {
    return this.remainingTasks != 0;
  }

  checkAll() {
    if (this.checked == false) {
      this.checked = true;
      this.array.forEach((task) => (task.completed = this.checked));
    } else {
      this.checked = false;
      this.array.forEach((task) => (task.completed = this.checked));
    }
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
