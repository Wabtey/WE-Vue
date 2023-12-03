<template>
    <li>
      <h3>{{ title }}</h3>
      <p>État: {{ status }}</p>
      <p v-if="dueDate">Date d'échéance: {{ dueDate }}</p>
    </li>
  </template>
  
  <script lang="ts">
    import TodoStatus from './todo_status'

    export default class TodoItem {
        title: string;
        status: TodoStatus;
        dueDate?: string;
        

        constructor(title: string, status: TodoStatus, dueDate?: string) {
            this.title = title;
            this.status = status;
            this.dueDate = dueDate;
        }
    };

    // export default { TodoItem, TodoStatus };
  </script>
  