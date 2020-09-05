<template>
    <div class="inputBox shadow">
        <input type="text" v-model="newTodoITem" placeholder="Type what you have to do" @keyup.enter="addTodo">
        <span class="addContainer" @click="addTodo">
            <i class="addBtn fas fa-plus" aria-hidden="true"></i>
        </span>
    </div>
</template>

<script>
export default {
    data() {
        return {
            newTodoITem: ''
        }
    },
    methods: {
        addTodo() {
            // 저장발생이후 emit을 통해 addTodoEmit 이벤트로 상위에 올린다.
            if(this.newTodoITem !== "") {
                var value = this.newTodoITem && this.newTodoITem.trim();
                this.$emit('addTodoEmit', value);
                this.clearInput();
            }
        },
        clearInput() {
            this.newTodoITem = '';
        }
    }
}
</script>

<style scoped>
input:focus {
    outline: none;
}
.inputBox {
    background: white;
    height: 50px;
    line-height: 50px;
    border-radius: 5px;
}
.inputBox input {
    border-style: none;
    font-size: 0.9rem;
}
.addContainer {
    float: right;
    background: linear-gradient(to right, #6478FB, #8763FB);
    display: block;
    width: 3rem;
    border-radius: 0 5px 5px 0;
}
.addBtn {
    color: white;
    vertical-align: middle;
}
.closeModalBtn {
    color: #42b983;
}
</style>