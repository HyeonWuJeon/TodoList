- APP 에게 받은 텍스트를 todos 배열에 추가한다.
<template>
    <input  
    v-model="todoText"
    type="text" 
    class="w-100 p-2" 
    placeholder="Type todo"
    @keyup.enter="addTodo"
    > 
</template>

<script>
export default {
    data() {
        return {
            todoText: '',
        }
    },
    methods: {
        addTodo(e) {
            this.$emit('add-todo', e.target.value);
        }
    }
}
</script>

<style>

</style>