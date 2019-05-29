<template>
  <dev>
    <p>
      /users/_id.vue
    </p>
  </dev>
</template>

<script>
  export default {
    data () {
      return {
        userId : this.$route.params.id
      }
    }
  }
</script>
