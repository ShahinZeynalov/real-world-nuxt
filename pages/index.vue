<template lang="html">
  <div>
    <h1>Events</h1>
    <EventCard
      v-for="(event, index) in events"
      :key="index"
      :event="event"
      :data-index="index"
    />
  </div>
</template>

<script>
import { mapState } from 'vuex'
import EventCard from '~/components/EventCard.vue'
// import EventService from '~/services/EventService.js'
export default {
  components: {
    EventCard
  },
  async fetch(context) {
    try {
      await context.store.dispatch('events/fetchEvents')
    } catch (e) {
      context.error({
        statusCode: 503,
        message: `Unable to fetch events at this time. Please try again. ${e}`
      })
    }
  },
  // async asyncData(context) {
  //   try {
  //     const response = await EventService.getEvents()
  //     return {
  //       events: response.data
  //     }
  //   } catch (e) {
  //     context.error({
  //       statusCode: 503,
  //       message: 'Unable to fetch events at this time. Please try again.'
  //     })
  //   }
  // },
  computed: {
    ...mapState({
      events: (state) => state.events.events
    })
  },
  head() {
    return {
      title: 'Event Listing'
    }
  }
}
</script>

<style lang="css" scoped>
h1 {
  margin: 0;
}
</style>
