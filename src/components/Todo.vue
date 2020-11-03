- 부모인 TODOLIST 에게 데이터를 받아온다.
- check, delete 내용을 부모인 TODOLIST 에게 전해준다.

<template>
    <div class="mb-2 d-flex">
        <div>
             <input type="checkbox" :checked ="todo.checked" @change="toggleCheck">
        </div>
        <!-- {{ todo.checked }} -->
      <span
       class="ml-3 flex-grow-1" 
       :class="todo.checked ? 'text-muted': ''"
       :style="todo.checked ? 'text-decoration: line-through': ''"
       >{{ todo.text }}
       </span>
       <button class = "btn btn-danger btn-sm" @click="clickDelete">Delete</button>
    </div>    
</template>

<script>
export default {
    props: {  // 부모가 전달해준 데이터를 받아온다. : TODOLIST 로 부터 데이터를 받아온다.
        todo: {
            type: Object,
            required: true
        }
    },
    methods: {
        toggleCheck(e) {
            this.$emit('toggle-checkbox', { // 부모컴포넌트에 데이터를 전달해 준다.
                 id: this.todo.id,
                 checked: e.target.checked       
            })
        },
        clickDelete(){
            this.$emit('click-delete', this.todo.id);
        }
    }
}
</script>

<style>

</style>