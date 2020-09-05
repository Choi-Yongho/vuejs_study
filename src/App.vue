<template>
    <div id="app">
        <TodoHeader></TodoHeader>
        <TodoInput @addTodoEmit="addTodo"></TodoInput>  <!-- 하위 emit으로 넘긴 addTodofEmit 이벤트를 자신의 addTodo 메서드로 던진다. -->
        <TodoList :propsdata="todoItems" @removeTodoEmit="removeTodo"></TodoList>  <!-- 하위로 내려줄 propsdata를 셋팅한다. 이벤트도 위와 같이 받아서 처리한다. -->
        <TodoFooter @clearTodoEmit="clearTodo"></TodoFooter>    <!-- v-on 은 @ 로 대체 가능, v-bind 는 :로 대체 가능.  -->
    </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue'
import TodoInput from './components/TodoInput.vue'
import TodoList from './components/TodoList.vue'
import TodoFooter from './components/TodoFooter.vue'

export default {
    data() {
        return {
            todoItems: []
        }
    },
    created() {
        // 초기 로딩시 todoItems 를 셋팅한다. 
        if(localStorage.length > 0) {
            for(var i=0; i<localStorage.length; i++) {
                if(localStorage.key(i) != "loglevel:webpack-dev-server") {
                    this.todoItems.push(localStorage.key(i));
                }
            }
        }
    },
    methods: {
        addTodo(value) {
            // 하위에서 던진 이벤트를 통해 저장 기능을 처리한다. 
            localStorage.setItem(value, value);
            this.todoItems.push(value);
        },
        removeTodo(todoItem, idx) {
            // 하위에서 던진 이벤트를 통해 삭제 기능을 처리한다. 
            localStorage.removeItem(todoItem);
            this.todoItems.splice(idx, 1);
        },
        clearTodo() {
            localStorage.clear();
            this.todoItems = [];
        }
    },
    components : {
        TodoHeader,     // TodoHeader : TodoHeader   >>  양쪽 변수와 객체 명이 같을경우 한개로 축약 사용 가능.
        TodoInput,
        TodoList,
        TodoFooter
    }
}
</script>

<style>
body {
    text-align : center;
    background-color : #F6F6F6;
}
input {
    border-style : groove;
    width : 200px;
}
button {
    border-style : groove;
}
.shadow {
    box-shadow : 5px 10px 10px rgba(0, 0, 0, 0.03);
}
</style>
