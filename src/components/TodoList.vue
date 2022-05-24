<template>
    <div>
        <ul>
            <TodoItem
                v-for="(todo, i) of todos"
                :todo="todo"
                :index="i"
                :key="i"
                v-on:remove-todo="removeTodo"
                v-on:changeCompleted="changeCompleted"
            />
        </ul>
    </div>
</template>

<script>
    import TodoItem from "@/components/TodoItem";

    export default {
        props: ['todos'],
        components: {
            TodoItem,
        },
        methods: {
            removeTodo(id){
                this.$emit('remove-todo', id);
            },
            changeCompleted(id){
                this.$emit('changeCompleted', id);
            }
        }
    }
</script>

<style scoped>
    ul{
        list-style: none;
        padding: 0;
        margin: 0;
    }
</style>