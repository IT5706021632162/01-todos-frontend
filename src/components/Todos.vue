<template>
  <div>
    <div v-for="(todo, index) in filterTodo" :key="todo.title" v-if="visibility === 'all'">
      <b-field class="is-pulled-left">
        <b-checkbox size="is-large"  :value="todo.completed" @input="statusTodo(index)">
        <strike v-if="todo.completed">{{ todo.title }}</strike>
        <p v-else> {{ todo.title }} </p>
        </b-checkbox>
      </b-field>
      <a class="delete is-pulled-right" @click="delTodo(index)" ></a>
      <div class="is-clearfix"></div>
    </div>

    <div v-for="(todo, index) in filterTodo" :key="todo.title" v-if="visibility === 'active'" v-show="!todo.completed">
      <b-field class="is-pulled-left">
        <b-checkbox size="is-large"  :value="todo.completed" @input="statusTodo(index)">
        <strike v-if="todo.completed">{{ todo.title }}</strike>
        <p v-else> {{ todo.title }} </p>
        </b-checkbox>
      </b-field>
      <a class="delete is-pulled-right" @click="delTodo(index)" ></a>
      <div class="is-clearfix"></div>
    </div>

    <div v-for="(todo, index) in filterTodo" :key="todo.title" v-if="visibility === 'completed'" v-show="todo.completed">
      <b-field class="is-pulled-left">
        <b-checkbox size="is-large"  :value="todo.completed" @input="statusTodo(index)">
        <strike v-if="todo.completed">{{ todo.title }}</strike>
        <p v-else> {{ todo.title }} </p>
        </b-checkbox>
      </b-field>
      <a class="delete is-pulled-right" @click="delTodo(index)" ></a>
      <div class="is-clearfix"></div>
    </div>
  </div>
</template>

<script>
import { mapGetters, mapActions } from 'vuex'

export default {
  computed: {
    ...mapGetters([
      'todos',
      'visibility'
    ]),
    filterTodo: function () {
      if (this.visibility === 'active') {
        return this.todos.filter(todo => todo.completed === false)
      } else if (this.visibility === 'completed') {
        return this.todos.filter(todo => todo.completed === true)
      } else if (this.visibility === 'ClearCompleted') {
        for (let i = this.todos.length - 1; i >= 0; i--) {
          if (this.todos[i].completed) {
            this.todos.splice(i, 1)
          }
        }
      } else return this.todos
    }
  },
  methods: {
    ...mapActions([
      'delTodo',
      'statusTodo',
      'visibility'
    ])
  }
}
</script>
