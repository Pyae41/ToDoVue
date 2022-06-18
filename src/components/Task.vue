<template lang="">
    <li class="flex justify-between items-center border border-gray-200 p-5 rounded-md">
        <input type="checkbox" class="border-gray-200 rounded
        focus:ring-transparent"
        v-model="completed"
        @change="updateTask()"/>
        <h3 :class="(completed)? 'line-through':'block'"> {{ task.task }}</h3>
        <a 
        @click="deleteTask()"
        class="px-2 py-1 bg-red-500 text-white rounded">
            <i class="fa-solid fa-trash-can"></i>
        </a>
    </li>
</template>


<script>
import axios from 'axios'

export default {
    props:['task'],
    data(){
        return{
            completed: '',
        }
    },
    name:'TaskVue',
    methods:{
        updateTask(){
            axios.put(`http://localhost:3000/tasks/${this.task.id}`,{
                'task': this.task.task,
                'completed': this.completed
            })
            .then(res => {
                if(res.status === 200){
                    this.$emit('updated')
                }
            })
            .catch(err => {
                console.log(err);
            });
        },
        deleteTask(){
            axios.delete(`http://localhost:3000/tasks/${this.task.id}`)
            .then(res => {
                if(res.status === 200){
                    this.$emit('deleted');
                }
            })
            .catch(err => {
                console.log(err);
            });
        }
    }
    
}
</script>
<style lang="">
    
</style>