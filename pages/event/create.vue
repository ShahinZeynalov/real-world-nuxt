<template lang="html">
  <div>
    <h1>Create an event</h1>
  </div>
</template>
<script>
export default {
  head() {
    return {
      title: 'Create an event',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'You can create a new event in your neighbourhood'
        }
      ]
    }
  }
}
</script>
<style lang="css" scoped>
h1 {
  display: block;
}
</style>
