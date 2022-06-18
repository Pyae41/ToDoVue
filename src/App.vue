<template>
  <div class="container m-auto">
     <div class="p-6 max-w-sm bg-white rounded-lg border border-gray-200 shadow-md m-auto mt-20">
    <AddVue
    @added="getTasks()"/>
  </div>
    <TaskViewVue
    :tasks="tasks"
    @deleteReload="getTasks()"
    @updateReload="getTasks()"/>
  </div>
</template>

<script>

import axios from 'axios'
import AddVue from './components/Add.vue'
import TaskViewVue from './components/TaskView.vue'

export default {
  name: 'App',
  data(){
    return{
      tasks:[]
    }
  },
  components: {
    AddVue,
    TaskViewVue
  },
  methods:{
    getTasks(){
        axios.get('http://localhost:3000/tasks')
        .then(res => {
            if(res.status === 200){
               this.tasks = res.data;
            }
        })
        .catch(err => {
          console.log(err);
        })
    }
  },
  created(){
    this.getTasks();
    
  }
}
</script>

<style>
</style>
