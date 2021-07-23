<template>
  <div class="health-check">
    <div
      v-if="successHealth()"
      class="success-health"
    />
    <div
      v-if="!successHealth()"
      class="error-health"
    />
  </div>
</template>

<script>
export default {
  name: 'HeathCheck',
  data () {
    return {
      apiHealthOk: false
    }
  },
  computed: {
  },
  mounted () {
    this.checkApiHealth()
  },
  methods: {
    successHealth () {
      return this.apiHealthOk
    },
    checkApiHealth () {
      const v = this
      setInterval(function () {
        v.httpApiHealth()
      }, 3000)
    },
    async  httpApiHealth () {
      try {
        const response = await fetch(
          'http://localhost:8090/health'
        )
        const data = await response
        // eslint-disable-next-line no-console
        console.log('LE FETCH FONCTIONNE', data)
        this.apiHealthOk = (data.status === 200)
      } catch (error) {
        this.apiHealthOk = false
        // eslint-disable-next-line no-console
        console.error('LE FETCH NE MARCHE PAS', error)
      }
    }
  }
}
</script>

<style scoped>
.health-check {
  display: flex;
}
.success-health, .error-health {
  border-radius: 25px;
  width: 25px;
  height: 25px;
  margin: 5px;
}
.success-health {
  background-color: green;
}

.error-health {
  background-color: red;
}

</style>
