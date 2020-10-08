<template>
<div id="app">
    <Header />
    <AddTodo v-on:add-todo="addTodo" />
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" v-on:mark-complete="markComplete" />
</div>
</template>

<script>
import Todos from './components/Todos.vue';
import AddTodo from './components/AddTodos';
import Header from './components/Header';

export default {
    name: 'App',
    components: {
        Todos,
        AddTodo,
        Header
    },
    data() {
        return {
            todos: [{
                    id: 1,
                    title: "Todo One",
                    completed: false
                },
                {
                    id: 2,
                    title: "Todo Two",
                    completed: true
                },
                {
                    id: 3,
                    title: "Todo Three",
                    completed: false
                },
            ]
        }
    },
    methods: {
        deleteTodo(id) {
            this.todos = this.todos.filter(todo => todo.id !== id);
        },
        markComplete(id) {
            // let obj = this.todos.filter(todo => todo.id == id);
            let elementsIndex = this.todos.findIndex(element => element.id == id)
            let newArray = [...this.todos];
            newArray[elementsIndex] = {
                ...newArray[elementsIndex],
                completed: !newArray[elementsIndex].completed
            }
            console.log(newArray)
            this.todos = newArray
            // https://medium.com/javascript-in-plain-english/react-updating-a-value-in-state-array-7bae7c7eaef9
        },
        addTodo(newTodo) {
            console.log(newTodo)
            this.todos = [...this.todos, newTodo];
        }
    }
}
</script>

<style>
* {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}

body {
    font-family: Arial, Helvetica, sans-serif;
    line-height: 1.4;
}
</style>
