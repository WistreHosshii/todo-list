<template>
    <div>
        TodoList
        <div v-for="task in tasks" :key="task.newTaskName">
            
        </div>
    </div>

    

</template>

<script>
export default {
    name: "ItemList",
    data(){
        return {
            newTaskName: "",
            isTaskDone:false,
            tasks:[
                {doTask:newTaskName, isDone:isTaskDone}
            ],
        };
    }
};
</script>

<style >
    
</style>