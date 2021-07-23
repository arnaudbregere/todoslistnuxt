<template>
  <div>
    <p>Coucou voici la list</p>
    <TodosMenu />
  </div>
</template>

<script>
import TodosMenu from '../components/TodosMenu'
export default {
  name: 'TodosList',
  components: { TodosMenu },
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
