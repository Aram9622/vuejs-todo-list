<template>
    <li>
        <span v-bind:class="{done: todo.completed}">
            <label>
                <input type="checkbox" v-model="todo.completed === true" checked v-on:change="changeCompleted(todo.id)">
            </label>
            <span class="block">
                <strong>{{index + 1}}</strong>
                <span class="title">{{todo.title}}</span>
            </span>

            <input type="hidden" v-model="title" class="hidden-title">
        </span>
        <div class="action">
            <button class="edit" @click="(e)=>{editTodo(todo.id, e)}">Edit</button>
            <button class="rm"  :disabled="todo.isEdit" v-on:click="$emit('remove-todo', todo.id)">&times;</button>
        </div>

    </li>
</template>

<script>
    export default {
        data(){
          return {
              title: ''
          }
        },
        props: {
            todo: {
                type: Object,
                required: true
            },
            index: {
                type: Number
            }
        },
        methods: {
            changeCompleted(id) {
                this.$emit('changeCompleted', id);
            },
            editTodo(id, e){
                let parent = e.target.closest('li');
                let titleText = parent.querySelector('.title');
                if(e.target.classList.contains('active')){
                    e.target.classList.remove('active')
                    e.target.innerHTML = 'Edit';
                    this.title = '';
                    this.todo.isEdit = false
                    parent.querySelector('.block').classList.remove('hide')
                    parent.querySelector('.hidden-title').setAttribute('type', 'hidden')
                }
                else {
                    e.target.classList.add('active');
                    e.target.innerHTML = 'Save';
                    this.title = titleText.innerHTML;
                    this.todo.isEdit = true
                    this.$emit('editTitle', this.todo);
                    parent.querySelector('.block').classList.add('hide')
                    parent.querySelector('.hidden-title').setAttribute('type', 'text')
                }

            }
        },
        mounted() {
            // this.todo.isEdit = false;
            console.log('mounted')
        },
        updated() {
            console.log('updated')
        },
        created() {
          console.log('created')
        },
        name: "TodoItem"
    }
</script>

<style scoped>
    li {
        border: 1px solid #ccc;
        display: flex;
        justify-content: space-between;
        padding: .5rem 2rem;
        margin-bottom: 1rem;
    }

    .rm {
        background: red;
        color: #fff;
        cursor: pointer;
        font-weight: bold;
    }

    input {
        margin-right: 1rem;
    }

    .done {
        text-decoration: line-through;
    }

    .action {
        display: flex;
    }
    .block.hide {
        display: none;
    }
</style>