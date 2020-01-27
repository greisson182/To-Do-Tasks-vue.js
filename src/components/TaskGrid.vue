<template>
    <div class="task-grid">
        <template v-if="tasks.length">
            <Taks 
                v-for="(task, i) in tasks" 
                :key="task.name"
                :task="task"
                @taskDeleted="$emit('taskDeleted', i)"
                @togleTaksState="$emit('togleTaksState', i)"
            ></Taks>    
        </template>
        <p v-else class="no-task">Sua vida está em dia :)</p>
    </div>
</template>

<script>
import Taks from './Task.vue';

export default {
    components: { Taks },
    props: {
        tasks: {type: Array, required: true }
    }
}
</script>

<style scoped>
    .task-grid {
        display: flex;
        justify-content: center;
        flex-wrap: wrap;
    }

     .task-grid .task{
        margin: 10px;
    }
</style>