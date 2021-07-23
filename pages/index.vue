<template>
  <div>
    <h1>Voici la page d'accueil de la Todo </h1>
    <TodosMenu />
    <HeathCheck />
  </div>
</template>
<script>
import TodosMenu from '../components/TodosMenu'
import HeathCheck from '../components/HeathCheck'
export default {
  components: { HeathCheck, TodosMenu }
}
</script>
