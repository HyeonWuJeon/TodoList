
<template>
<div>
  Completed Todo: {{numberOfCompletedTodo }}
</div>
</template>

<script>
export default {
    props:{
        todos:{
            type: Array,
            required: true

        }
    },
    computed: {
        numberOfCompletedTodo() {
            return this.todos.filter(todo => todo.checked).length;// 체크박스 클릭시 Completed 증가
        }
    }
}
</script>

<style>

</style>