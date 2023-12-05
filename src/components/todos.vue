<template>
    <div class="todos">
        <h1>Tasks list</h1>
        <input v-model="input_message" placeholder="Your task">
        <button v-on:click="add_task(input_message)">add</button>
    
        <li v-for="todo in todos_list"
            :key="todo.title"
        >
            <button v-on:click="complete_task(todo)" v-if="is_completed(todo)">x</button>
            <button v-on:click="complete_task(todo)" v-if="!is_completed(todo)">_</button>
            {{ todo.title }},
            {{ todo.status }}
        </li>
    </div>

    <!-- <li v-if="!todo.isComplete">
      {{ todo.title }}
    </li> -->
</template>
<script lang="ts">
    //class component

    import { Component, Vue, toNative } from 'vue-facing-decorator'
    import TodoItem from './TODOComponent.vue'
    import TodoStatus from './todo_status'
    @Component
    class Todos extends Vue {
        input_message = 'Be happy'

        todos_list: TodoItem[] = [
            new TodoItem('Make bread', TodoStatus.InProgress, '2024-02-10'),
            new TodoItem('Talk to Lou', TodoStatus.Completed, '2024-02-15'),
        ]

        add_task(message: string): void {
            if (message != '') {
                this.todos_list.push(new TodoItem(message, TodoStatus.InProgress))
            }
        }
        
        /**
         * If `TodoStatus.Idle` or `TodoStatus.InProgress`,
         * switch the todo to `TodoStatus.Completed`.
         * Else into `TodoStatus.InProgress`.
         * 
         * @param todo the todo item to change
         */
        complete_task(todo: TodoItem): void {
            if (todo.status == TodoStatus.Completed) {
                todo.status = TodoStatus.InProgress
            } else {
                todo.status = TodoStatus.Completed
            }
        }

        remove_task(todo: TodoItem): void {
            const index = this.todos_list.indexOf(todo, 0);
            if (index > -1) {
                this.todos_list.splice(index, 1);
            }
        }

        is_completed(todo: TodoItem): boolean {
            return todo.status == TodoStatus.Completed;
        }
    }
    export default toNative(Todos);
</script>
<style>
    /* .todos h1, */
    .todos input{
        text-align: center;
        /* justify-content: center; */
    }
</style>
