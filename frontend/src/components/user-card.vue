<script>
export default {
  name: 'UserCard',
  props: ['user'],
}
</script>

<template lang="pug">
.box
  h2 {{user.name}} {{user.age}}
    p(v-if="!user.email.length")
      | Should enter your email!!
    p(v-else)
      | {{ user.email}}


</template>

<style lang="scss" scoped>
.box {
  padding: 2rem;
  border: 1px solid black;
  border-radius: 0.3rem;
}
</style>
