<template>
    <div class="todos">
        <h1>Tasks list</h1>
        <input v-model="input_message" placeholder="Your task">
        <button v-on:click="add_task(input_message)">add</button>
        
        <br> Special Actions:
        <button v-on:click="clear_tasks()">&#9888; clear all</button>
        <button v-on:click="clear_completed()">&#9888; clear completed</button>


        <br> filters: 
        <button v-on:click="display_all_task()">All task</button>
        <button v-on:click="display_completed_task()">Completed task</button>
        <button v-on:click="display_in_progress_task()">InProgress task</button>
        
        <ul v-if="is_display_all() || is_display_in_progress()">
            <li v-for="todo in inProgressTodos"
                :key="todo.title"
            >
                <!-- <button v-on:click="complete_task(todo)" v-if="is_completed(todo)">x</button> -->
                <button v-on:click="remove_task(todo)">🗑️</button>
                <button v-on:click="complete_task(todo)">_</button>
                {{ todo.title }},
                {{ todo.status }}
            </li>
        </ul>
        
        <ul v-if="is_display_all() || is_display_completed()">
            <li v-for="todo in completedTodos"
            :key="todo.title"
            >
                <button v-on:click="remove_task(todo)">🗑️</button>
                <button v-on:click="complete_task(todo)">x</button>
                {{ todo.title }},
                {{ todo.status }}
            </li>
        </ul>

        <footer v-if="todos_list.length > 0">
          <p>
            You have <span class="highlight">{{ todos_list.length }}</span> todos.
          </p>
        </footer>
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
    import FilterMode from './filter_mode'
    
    @Component
    class Todos extends Vue {
        input_message = 'Be happy'
        filterMode: FilterMode = FilterMode.DisplayAll

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

        clear_tasks(): void {
            // TODO: add warning popup
            this.todos_list = []
        }

        clear_completed(): void {
            // TODO: add warning popup
            this.todos_list = this.todos_list.filter(this.is_not_completed);
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

        is_not_completed(todo: TodoItem): boolean {
            return todo.status != TodoStatus.Completed;
        }

        /* --------------------------------- Filters -------------------------------- */

        // --- setters ---

        display_all_task(): void {
            this.filterMode = FilterMode.DisplayAll
        }

        display_completed_task(): void {
            this.filterMode = FilterMode.DisplayCompleted
        }

        display_in_progress_task(): void {
            this.filterMode = FilterMode.DisplayInProgress
        }

        // --- getters ---
        
        get inProgressTodos(): TodoItem[] {
            return this.todos_list.filter((todo) => !this.is_completed(todo));
        }

        get completedTodos(): TodoItem[] {
            return this.todos_list.filter(this.is_completed);
        }

        is_display_all(): boolean {
            return this.filterMode == FilterMode.DisplayAll
        }
        is_display_completed(): boolean {
            return this.filterMode == FilterMode.DisplayCompleted
        }
        is_display_in_progress(): boolean {
            return this.filterMode == FilterMode.DisplayInProgress
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

    footer {
        /* background-color: #f0f0f0; */
        padding: 10px;
        text-align: center;
    }
</style>
