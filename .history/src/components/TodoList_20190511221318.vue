<template>
    <div>
        <div>TodoList</div>
        <div v-for="task in tasks" :key="task.doTask">
            <div class="name">タスク: {{task.doTask}} </div>
            
        </div>
    </div>

    

</template>

<script>
export default {
    name: "ItemList",
    let list = new
    data(){
        return {
            newTaskName: "",
            isTaskDone:false,
            tasks:[
                {doTask:'newTaskName', isDone:isTaskDone}
            ],
        };
    }
};
</script>

<style >
    
</style>