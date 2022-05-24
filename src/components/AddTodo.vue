<template>
    <div class="form">
        <form action="" @submit.prevent="onSubmit">
            <input type="text" v-model="title">
            <button type="submit">Create</button>
        </form>
        <SortTodo
            @get-limit="getLimit"
        />
    </div>

</template>

<script>
    import SortTodo from "./SortTodo";

    export default {
        data() {
            return {
                title: '',
            }
        },
        components: {
          SortTodo
        },
        methods: {
            onSubmit(){
                if(this.title.trim()){
                    const newTodo = {
                        id: Date.now(),
                        title: this.title,
                        completed: false
                    }

                    this.$emit('add-todo', newTodo)
                    this.title = '';
                }
            },
            getLimit(limit){
                this.$emit('limit', limit);
            }
        }
    }
</script>

<style scoped>
    .form {
        display: flex;
    }
    input {
        width: 400px;
    }
</style>