<template>
    <select id="sort" @change="selectSort" v-model="limit">
        <option value="0" selected>None</option>
        <option v-for="item of limitArray" :value="item">{{item}}</option>
    </select>
</template>

<script>
    export default {
        data(){
          return {
              limit: 0,
              limitArray: [3, 5, 10, 15, 20, 25, 50, 100, 150, 200]
          }
        },
        computed:{
          filterItems() {
              this.items.filter(item => {
                  return item.name = this.inputVal
              })
          }
        },
        methods: {
            selectSort(){
                console.log(this.limit)
                this.$emit('get-limit', this.limit == 0 ? 5 : this.limit)
            }
        }
    }
</script>

<style scoped>

</style>