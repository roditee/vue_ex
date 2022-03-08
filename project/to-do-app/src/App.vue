<template>
  <div id="app">
    <TodoHeader></TodoHeader>
    <!-- 할 일 추가 버튼 클릭했을 때 App 컴포넌트로 이벤트 전달할 수 있도록 v-on 디렉티브 추가  -->
    <TodoInput v-on:addTodo="AddTodo"></TodoInput>
    <TodoList v-bind:propsdata="todoItems" @removeTodo="removeTodo"></TodoList>
    <TodoFooter v-on:removeAll="clearAll"></TodoFooter>
  </div>
</template>

<script>
import TodoHeader from "./components/TodoHeader.vue";
import TodoInput from "./components/TodoInput.vue";
import TodoList from "./components/TodoList.vue";
import TodoFooter from "./components/TodoFooter.vue";

export default {
  name: "app",
  data() {
    return {
      todoItems: [],
    };
  },
  created() {
    // 로컬 스토리지에서 데이터 읽어서 배열에 저장
    if(localStorage.length > 0) {
      for (var i=0; i<localStorage.length; i++) {
        this.todoItems.push(localStorage.key(i));
      }
    }
  },
  method: {
    addTodo(todoItem) {
      localStorage.setItem(todoItem, todoItem);
      this.todoItems.push(todoItem);
    },
    removeTodo(todoItem, index) {
        localStorage.removeItem(todoItem);
        this.todoItems.splice(index, 1);
    },
    clearAll() {
      localStorage.clear();
      this.todoItems = [];
    }
  },
  components: {
    TodoHeader: TodoHeader,
    TodoInput: TodoInput,
    TodoList: TodoList,
    TodoFooter: TodoFooter,
  },
};
</script>

<style>
body {
  text-align: center;
  background-color: #f6f6f8;
}
input {
  border-style: groove;
  width: 200px;
}
button {
  border-style: groove;
}
.shadow {
  box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03);
}
</style>