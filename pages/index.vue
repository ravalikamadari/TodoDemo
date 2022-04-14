<template>
  <div>
    <LoginForm v-if="token == null" />

    <div class="todo-list" v-if="todos.length > 0">
    <div>
       <div id="todo" class="header">
        <!-- <h2>My Todos</h2> -->
        <input type="text" id="task" placeholder="Title..." v-model="todo" />
        <span @click="addTodo(todo)" class="addBtn">Add New</span>
  </div>
    </div>

      <TodoItem v-for="item in todos" :key="item.id" :item="item" />
    </div>
  </div>
</template>

<script>
import { mapState } from 'vuex'

import LoginForm from '@/components/LoginForm.vue'
import TodoItem from '@/components/Todo.vue'

export default {
  name: 'IndexPage',

  components: {
    LoginForm,
    TodoItem,
  },

  computed: {
    ...mapState(['token', 'todos']),
  },
   data() {
        return {
            todo: '',
        }
    },

    methods: {

     async   addTodo(todo) {
          await  this.$store.dispatch('addTodo', todo);
          await  this.$store.dispatch('getAllTodos');
        },
    }

}
</script>
<style scoped>

.addBtn {
  padding: 10px;
  width: 25%;
  background: #d9d9d9;
  color: #555;
  float: left;
  text-align: center;
  font-size: 16px;
  cursor: pointer;
  transition: 0.3s;
  border-radius: 0;
}

.addBtn:hover {
  background-color: #bbb;
}
.header {
  background-color: #fdfdfd;
  padding: 5px 40px;
  color: white;
  text-align: center;
}

/* Clear floats after the header */
.header:after {
  content: "";
  display: table;
  clear: both;
}
</style>
