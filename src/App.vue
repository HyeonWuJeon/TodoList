<template>
  <div id = 'app' class ='container'>
    <h1 class='text-center'>Todo App</h1>
    <input 
    v-model="todoText"
    type="text" 
    class="w-100 p-2" 
    placeholder="Type todo"
    @keyup.enter="addTodo"
    >
    <!-- <button @click="addTodo">Click</button>  -->
    <hr>
    <!-- Todo  컴포넌트를 사용하고  todos의 데이터를 뿌려준다 / 자식데이터를 가져온다. -->
    <Todo v-for="todo in todos"  
    :key="todo.id"
    :todo="todo"
    @toggle-checkbox ="toggleCheckbox"
    @click-delete = "deleteTodo"
    />
      
  </div>
</template>

<script>
import Todo from '@/components/Todo.vue';
export default {
  components:{
    Todo
  },
  data() {
    return {
      todoText: '',
      todos: [
        {id: 1, text: 'buy a car', checked: false},
        {id: 2, text: 'play game', checked: false},

      ]
    }
  },

  methods:{
    deleteTodo(id) {
      // const index = this.todos.findIndex(todo => {
      //   return todo.id ===id;
      // });
      // this.todos.splice(index, 1); // 삭제할 인덱스, 1개
      this.todos = this.todos.filter(todo => todo.id !== id); // 입력값을 제외한 나머지값을 배열에 채워준다.

    },
    addTodo(e) {
      console.log(e.target.value);
      this.todos.push({
        id: Math.random(),
        text: e.target.value,
        checked: false
      });
      this.todoText='';
    },
    
    toggleCheckbox({id, checked}) { //구조분해
      console.log(id, checked);
      const index = this.todos.findIndex(todo => { //  todos 배열에서 id 인덱스가 같은걸 찾아준다.
        return todo.id ===id;
      });
      this.todos[index].checked = checked; // 찾은값을 바꾼값으로 변경시킨다.
    }
  }
}
</script>
