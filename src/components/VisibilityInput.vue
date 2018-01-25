<template>
  <div>
    <b-field class="is-pulled-right">
      <b-radio-button v-model="visibility"
        native-value="all">
        <span>All ( {{all}})</span>
      </b-radio-button>
      <b-radio-button v-model="visibility"
        native-value="active">
        <span>Active ( {{active}} )</span>
      </b-radio-button>
      <b-radio-button v-model="visibility"
        native-value="completed">
        <span>Completed ( {{Completed}} )</span>
      </b-radio-button>
      <b-radio-button v-model="visibility"
        native-value="ClearCompleted" >
        <span>Clear Completed</span>
      </b-radio-button>
    </b-field>
  </div>
</template>

<script>
import { store } from '@/store'
import { mapGetters } from 'vuex'
export default {
  computed: {
    ...mapGetters([
      'todos',
      'visibility'
    ]),
    all () {
      if (this.todos) {
        return this.todos.length
      }
    },
    active () {
      if (this.todos) {
        return this.todos.filter(todo => todo.completed === false).length
      }
    },
    Completed () {
      if (this.todos) {
        return this.todos.filter(todo => todo.completed === true).length
      }
    },
    visibility: {
      get: function () {
        return store.state.visibility
      },
      set: function (newValue) {
        store.dispatch('changeVisibility', newValue)
      }
    }
  }
}
</script>
