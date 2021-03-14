<template>
    <li>
        <span v-bind:class="{done: todo.completed}">
            <input type="checkbox" :value="todo.completed"
                   v-on:change="todo.completed = !todo.completed">
            <strong>{{ index + 1 }}</strong>
            {{ todo.title | uppercase}}
        </span>
        <button class="rm" v-on:click="$emit('remove-todo', todo.id)">&times;</button>
    </li>
</template>

<script>
export default {
    props: {
        todo: {
            type: Object,
            required: true
        },
        index: Number
    },
    filters: {
        uppercase(value) {
            return value.toUpperCase()
        }
    }
}
</script>

<style scoped>
li {
    display: flex;
    align-items: center;
    justify-content: space-between;
    border: 1px solid #ccc;
    border-radius: 4px;
    padding: .5rem 1rem;
    margin-bottom: .5rem;
}

li span {
    text-align: left;
}

input {
    margin-right: 1rem;
}

.rm {
    background: #a41515;
    border-radius: 100%;
    color: #fff;
    font-size: 1.5rem;
    border: none;
    width: 1.5rem;
    height: 1.5rem;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    outline: none;
}

.done {
    text-decoration: line-through;
}
</style>