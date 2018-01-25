<template>
  <div>
    <p class="is-pulled-left"  v-if="visibility === 'all'">{{count}} items left</p>
    <p class="is-pulled-left"  v-if="visibility === 'active'">{{count}} items left</p>
    <p class="is-pulled-left"  v-if="visibility === 'completed'" >{{count}} items left</p>

    <visibility-input/>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
import VisibilityInput from '@/components/VisibilityInput'

export default {
  components: {
    VisibilityInput
  },
  data () {
    return {
      status: 'All'
    }
  },
  computed: {
    ...mapGetters([
      'todos',
      'visibility'
    ]),
    count () {
      if (this.visibility === 'active') {
        return this.todos.filter(todo => todo.completed === false).length
      } else if (this.visibility === 'completed') {
        return this.todos.filter(todo => todo.completed === true).length
      } else if (this.visibility === 'all') {
        return this.todos.length
      }
    }
  }
}
</script>
