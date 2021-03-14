<template>
    <div>
        <router-link to="/" class="back">Home</router-link>
        <h2>Todo list</h2>
        <AddTodo @add-todo="addTodo"/>
        <select v-model="filter">
            <option value="all">All</option>
            <option value="completed">Completed</option>
            <option value="not-completed">Not completed</option>
        </select>
        <hr>
        <div class="wrapper">
            <Loader v-if="loading"/>
            <TodoList
                v-else-if="filteredTodos.length"
                v-bind:todos="filteredTodos"
                @remove-todo="removeTodo"
            />
            <p v-else>No todos</p>
        </div>
    </div>
</template>

<script>
import TodoList from '@/components/TodoList'
import AddTodo from '@/components/AddTodo';
import Loader from '@/components/Loader';

export default {
    name: 'Todos',
    data: () => ({
        todos: [],
        loading: true,
        filter: 'all'
    }),
    components: {
        Loader,
        TodoList,
        AddTodo
    },
    mounted() {
        fetch('https://jsonplaceholder.typicode.com/todos/?_limit=3')
            .then(response => response.json())
            .then(json => {
                this.todos = json
                this.loading = false
            })
    },
    // watch: {
    //     filter(value) {
    //         console.log(value)
    //     }
    // },
    computed: {
        // аля переменная для вывода todos
        filteredTodos() {
            if (this.filter === 'all') {
                return this.todos
            }

            if (this.filter === 'completed') {
                return this.todos.filter(item => item.completed)
            }

            if (this.filter === 'not-completed') {
                return this.todos.filter(item => !item.completed)
            }
        }
    },
    methods: {
        removeTodo(id) {
            this.todos = this.todos.filter(item => item.id !== id)
        },
        addTodo(todo) {
            this.todos.push(todo)
        }
    }
}
</script>

<style>
.back {

}
</style>