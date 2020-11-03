- App.vue에서 데이터를 받아서 화면에 뿌려준다.
- 체크기능과 삭제기능이 있다.
- 삭제를 하기위한 데이터는 자식인 TODO 한테 받는다.
- 반대로 부모가된 TODO는 자신의 부모인 APP에게서 받은 데이터를 자식인 TODO에게 뿌려준다.
<template>
    <div>
        <!-- TODOLIST가 부모가되어 TODO에게 데이터를 던져준다. -->
   <Todo v-for="todo in todos"  
    :key="todo.id"
    :todo="todo"
    @toggle-checkbox ="toggleCheckbox"
    @click-delete = "deleteTodo"
    /> 
   <hr>
    </div>
</template>

<script>
import Todo from '@/components/Todo.vue'
export default {
    components: {
        Todo
    }, 
    // 부모의 todos 를 받을 props
    props:{
        todos : {
            type: Array,
            required: true
        }
    }, 
    methods : { // TODO -> TODOLIST -> APP
        toggleCheckbox(value){
            this.$emit('toggle-checkbox', value); // 체크박스 유무

        },
        deleteTodo(todoId){
            this.$emit('click-delete', todoId); // 아이디값
        }
    }
}
</script>

<style>

</style>