<template lang="">
    <ul v-for="(task,index) in tasks" :key="index"
    class="w-96 m-auto mt-2 shadow-lg">
        <TaskVue
        :task="task"
        @deleted="$emit('deleteReload')"
        @updated="$emit('updateReload')"/>
    </ul>
</template>


<script>
import TaskVue from './Task.vue'


export default {
    props:['tasks'],
    name:'TaskViewVue',
    components:{
        TaskVue
    }
    
}
</script>
<style lang="">
    
</style>