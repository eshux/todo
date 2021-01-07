<template>
  <section class="section">
    <div class="container container-fluid">
      <div class="row center-xs">
        <div class="col-xs-12">
          <div class="wrapper">
            <div v-if="show === 'all'">
              <Button
                @click="show = 'unfinished'"
                label="Unfinished tasks"
                :active="show === 'unfinished' && true"
              />
              <Button
                @click="show = 'finished'"
                label="Finished tasks"
                :active="show === 'finished' && true"
              />
            </div>

            <div v-else>
              <Button
                @click="show = 'unfinished'"
                label="Unfinished tasks"
                :active="show === 'unfinished' && true"
              />
              <Button
                @click="show = 'finished'"
                label="Finished tasks"
                :active="show === 'finished' && true"
              />
              <Button @click="show = 'all'" label="All tasks" :active="show === 'all' && true" />
            </div>

            <form
              class="form"
              @submit.prevent="
                addTodo({
                  id: inputValue + todos.length + random(),
                  value: inputValue,
                  isDone: false,
                }),
                  changeInput('')
              "
            >
              <input
                type="text"
                class="input"
                :value="inputValue"
                placeholder="Add a new task"
                @change="changeInput($event.target.value)"
              />
              <Button type="fill" label="Add" />
            </form>

            <Todo
              v-for="todo in filteredTodos"
              :key="todo.id"
              :id="todo.id"
              :checkboxValue="todo.isDone"
              :todo="todo.value"
              @onChange="changeDone(todo.id)"
              @onClick="deleteTodo(todo.id)"
            />
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script lang="ts">
/* eslint-disable no-param-reassign */
import { defineComponent } from 'vue';
import Todo from './components/Todo/Todo.vue';
import Button from './components/Button/Button.vue';
import todoData from './data/data';

type Data = {
  inputValue: string;
  todos: Todo[];
  show: 'all' | 'unfinished' | 'finished';
};

type Todo = {
  id: string;
  value: string;
  isDone: boolean;
};

const App = defineComponent({
  components: {
    Todo,
    Button,
  },

  data(): Data {
    return {
      inputValue: '',
      todos: todoData,
      show: 'all',
    };
  },

  methods: {
    changeInput(value: string) {
      this.inputValue = value;
    },

    addTodo(todo: Todo) {
      if (todo.value) {
        this.todos.push(todo);
      }
    },

    changeDone(id: string) {
      return this.todos.map((todo) => {
        if (todo.id === id) {
          todo.isDone = !todo.isDone;
        }
        return todo;
      });
    },

    deleteTodo(id: string) {
      const i = this.todos.findIndex((todo) => todo.id === id);
      this.todos.splice(i, 1);
    },

    random() {
      return Math.floor(Math.random() * 100);
    },
  },

  computed: {
    filteredTodos(): Todo[] {
      return this.todos.filter((todo: Todo) => {
        switch (this.show) {
          case 'unfinished':
            return !todo.isDone;
          case 'finished':
            return todo.isDone;
          default:
            return todo;
        }
      });
    },
  },
});

export default App;
</script>

<style src="./app.scss" lang="scss"></style>
