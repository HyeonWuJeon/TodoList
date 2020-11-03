<template>
  <div id = 'app' class ='container'>
    <h1 class='text-center'>Todo App</h1>
    <!-- 자식에서 올라온 이벤트를 받는다. -->
    <AddTodo @add-todo="addTodo"/> 
    <CompletedTodo :todos ='todos'/>
    <!-- <input  AddTodo.vue 로 이동
    v-model="todoText"
    type="text" 
    class="w-100 p-2" 
    placeholder="Type todo"
    @keyup.enter="addTodo"
    > -->
    <hr>
    <!-- Todo  컴포넌트를 사용하고  todos의 데이터를 뿌려준다 / 자식에게 데이터전송, @ : 자식데이터를 가져온다. -->
    <!-- <Todo v-for="todo in todos"  
    :key="todo.id"
    :todo="todo"
    @toggle-checkbox ="toggleCheckbox"
    @click-delete = "deleteTodo"
    /> -->
      <TodoList  :todos="todos"
      @toggle-checkbox="toggleCheckbox"
      @click-delete="deleteTodo"
      />
  </div>
</template>

<script>
// import Todo from '@/components/Todo.vue';
import TodoList from '@/components/TodoList';
import AddTodo from '@/components/AddTodo'; 
import CompletedTodo from '@/components/CompletedTodo';
export default {
  components:{
    TodoList,
    AddTodo,
    CompletedTodo
    // Todo
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
      this.todos = this.todos.filter(todo => todo.id !== id); // 입력값을 제외한 나머지값을 배열에

    },
    addTodo(value) {
      console.log(value);
      this.todos.push({
        id: Math.random(),
        text: value,
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
