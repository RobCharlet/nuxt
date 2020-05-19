<template>
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
import EventCard from '~/components/EventCard'
import EventService from '~/services/EventService'
export default {
  components: {
    EventCard
  },
  // Called each time before the page component is loaded
  async asyncData({ error }) {
    try {
      const { data } = await EventService.getEvents()
      return {
        // merges with component data
        events: data
      }
    } catch (e) {
      error({
        statusCode: 503,
        message: 'Unable to fetch events at this time. Please try again.'
      })
    }
  },
  head() {
    return {
      title: 'Event Listening'
    }
  }
}
</script>
