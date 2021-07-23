<template>
  <div>
    <p>Coucou voici la list</p>
    <TodosMenu />
    <HeathCheck />
  </div>
</template>

<script>
import TodosMenu from '../components/TodosMenu'
import HeathCheck from '../components/HeathCheck'
export default {
  name: 'TodosList',
  components: { HeathCheck, TodosMenu },
  props: ['todos'],
  data () {
    return {
      editing: null
    }
  },

  mounted () {

  },
  methods: {
    editMode (title) {
      this.editing = title
    },

    editTodo (todo) {
      if (todo.title === '' || todo.id === '' || todo.description || todo.dueDate) { return }
      this.$emit('edit:todo', todo.title, todo)
      this.editing = null
    }
  }
}
</script>

<style scoped>
button {
  margin: 0 0.5rem 0 0;
}

input {
  margin: 0;
}

.empty-table {
  text-align: center;
}
</style>
