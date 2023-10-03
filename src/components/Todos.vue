<template >
    <main class="flex justify-center items-center h-screen">
        <div class="w-2/3 md:w-2/4">
            <input
              type="text"
              placeholder="Todo"
              v-model="todoText"
              class="border  h-10 px-3 rounded focus:outline-none w-10/12"
            >
            <button
              class="bg-black h-10 rounded w-10 text-white font-bold ml-7"
              @click="addTodo"
            >+</button>
            <div v-for="todo in todoList" :key="todo.id" class="w-full border rounded h-10 flex items-center justify-between mt-5 px-5" @click="toggleIsDone(todo.id)">
                <p >{{todo.value}}</p>
                <p>{{todo.isDone ? "Finished" : "Unfinished"}}</p>
            </div>
        </div>
    </main>
</template>
<script>
import { ref } from "vue";
export default {

    setup() {
        const todoList = ref([]);
        const todoText = ref('')


        const addTodo = () => {
            todoList.value.push({
                value: todoText.value,
                isDone: false,
                id: Math.random() * 10000000
            })
            todoText.value = ''
        }

        const toggleIsDone = (id) => {
            const matchingId = todoList.value.filter((todo) => todo.id === id)

            if (matchingId.length === 0) {
                return
            }

            const  todoItem =  matchingId[0]

            todoItem.isDone = !todoItem.isDone
        }


        return{todoList, todoText, addTodo, toggleIsDone, deleteTodo}
    }
}
</script>