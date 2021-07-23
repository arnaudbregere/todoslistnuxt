<template>
  <div id="todo-form">
    <form @submit.prevent="handleSubmit">
      <label>Todo Title</label>
      <input
        ref="first"
        v-model="todo.title"
        type="text"
        :class="{ 'has-error': submitting && invalidTitle }"
        @keypress="clearStatus"
      >
      <label>Todo Description</label>
      <input
        v-model="todo.description"
        type="text"
        :class="{ 'has-error': submitting && InvalidDescription }"
        @focus="clearStatus"
        @keypress="clearStatus"
      >
      <label>Todo DueDate</label>
      <input
        v-model="todo.dueDate"
        type="number"
        :class="{ 'has-error': submitting && InvalidDueDate }"
        @focus="clearStatus"
        @keypress="clearStatus"
      >
      <p v-if="error && submitting" class="error-message">
        /!\ Remplissez tous les champs !
      </p>
      <p v-if="success" class="success-message">
        ✅ Todo ajoutée avec Succès !!
      </p>
      <button>Ajouter Todo</button>
    </form>
    <TodosMenu />
  </div>
</template>

<script>
import TodosMenu from '../components/TodosMenu'
export default {
  name: 'TodosForm',
  components: { TodosMenu },
  data () {
    return {
      error: false,
      submitting: false,
      success: false,
      todo: {
        title: '',
        description: '',
        dueDate: ''
      }
    }
  },
  computed: {
    invalidTitle () {
      return this.todo.title === ''
    },

    invalidDescription () {
      return this.todo.description === ''
    },

    invalidDueDate () {
      return this.todo.dueDate === ''
    },

    invalidId () {
      return this.todo.id === ''
    }
  },
  methods: {
    handleSubmit () {
      this.clearStatus()
      this.submitting = true

      if (this.invalidTitle || this.invalidId || this.invalidDueDate || this.invalidDescription) {
        this.error = true
        return
      }

      this.$emit('add:todo', this.todo)
      this.$refs.first.focus()
      this.todo = {
        title: '',
        id: '',
        description: '',
        dueDate: ''
      }
      this.clearStatus()
      this.submitting = false
    },

    clearStatus () {
      this.success = false
      this.error = false
    }
  }
}
</script>

<style scoped>
form {
  margin-bottom: 2rem;
}

[class*="-message"] {
  font-weight: 500;
}

.error-message {
  color: #d33c40;
}

.success-message {
  color: #32a95d;
}
</style>
