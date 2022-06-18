<template lang="">
    <div class="mb-10">
        <h3 class="text-3xl font-medium text-center">To Do List</h3>
    </div>
    <div class="max-w-100 flex justify-around items-center">
        <input type="text" v-model="task.task" placeholder="Enter Task" class="font-medium border-gray-300 rounded focus:border-green-400"/>
        <a 
        @click="addTask()"
        class="px-3 py-2 rounded mx-5 bg-green-400 text-xl text-white">
            <i class="fa-solid fa-plus"></i>
        </a>
    </div>
    
</template>
<script>
import axios from 'axios';
export default {
    name: 'AddVue',
    data(){
        return{
            task:{
                task: '',
                completed: false
            }
        }
    },
    methods:{
        addTask(){
           if(this.task.task === ''){
               alert('Enter Task');
           }
           else{
               axios.post('http://localhost:3000/tasks',this.task)
               .then(res => {
                   if(res.status === 201){
                       this.task.task = '';
                       this.$emit('added');
                   }
               })
               .catch(err => {
                   console.log(err);
               })
           }
        }
    }
}
</script>
<style lang="">
    
</style>