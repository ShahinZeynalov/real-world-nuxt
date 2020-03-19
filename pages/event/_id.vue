<template lang="html">
  <div>
    <h1>{{ event }}</h1>
  </div>
</template>
<script>
import { mapState } from 'vuex'
// import EventService from '~/services/EventService.js'

export default {
  async fetch(context) {
    try {
      await context.store.dispatch('events/fetchEvent', context.params.id)
    } catch (e) {
      context.error({
        statusCode: 503,
        message: `Unable to fetch event #${context.params.id}`
      })
    }
  },
  // async asyncData(context) {
  //   try {
  //     const response = await EventService.getEvent(context.params.id)
  //     return {
  //       event: response.data
  //     }
  //   } catch (e) {
  //     context.error({
  //       statusCode: 503,
  //       message: `Unable to fetch event #${context.params.id}`
  //     })
  //   }
  // },
  computed: {
    ...mapState({
      event: (state) => state.events.event
    })
  },
  head() {
    return {
      title: this.event.title,
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: `What you need to know about event # ${this.event.title}`
        }
      ]
    }
  }
}
</script>
