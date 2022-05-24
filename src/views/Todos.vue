<template>
    <div>
        <h1>Todo application</h1>
        <AddTodo @add-todo="addTodo" @limit="limitData"/>
        <hr>
        <TodoList v-bind:todos="todos" @remove-todo="removeTodo" @changeCompleted="changeCompleted"/>

    </div>
</template>

<script>
    import TodoList from '@/components/TodoList'
    import AddTodo from "@/components/AddTodo";

    export default {
        name: 'App',
        data() {
            return {
                todos: [
                    {id: 1, title: 'Купить хлеб', completed: false},
                    {id: 2, title: 'Купить масло', completed: false},
                    {id: 3, title: 'Купить пиво', completed: false},
                ],
                limit: 3
            }
        },
        mounted() {
            fetch(`https://jsonplaceholder.typicode.com/todos?_limit=${this.limit}`)
                .then(response => response.json())
                .then(json => this.todos = json)
        },
        components: {
            TodoList,
            AddTodo
        },
        methods: {
            removeTodo(id){
                this.todos = this.todos.filter(item => item.id !== id)
            },
            addTodo(todo){
                this.todos.push(todo)
            },
            changeCompleted(id){
                this.todos = this.todos.map((item)=>{
                    if(item.id === id){
                        item.completed = !item.completed
                    }
                    return item
                });
            },
            limitData(limit){
                fetch(`https://jsonplaceholder.typicode.com/todos?_limit=${limit}`)
                    .then(response => response.json())
                    .then(json => this.todos = json)
            }
        }
    }
</script>

<style scoped>

</style>