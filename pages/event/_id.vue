<template>
  <div>
    <h1>{{ event.title }}</h1>
  </div>
</template>

<script>
import EventService from '~/services/EventService'
export default {
  async asyncData({ error, params }) {
    try {
      const { data } = await EventService.getEvent(params.id)
      return {
        // merges with component data
        event: data
      }
    } catch (e) {
      error({
        statusCode: 503,
        message: 'Unable to fetch event #' + params.id
      })
    }
  },
  head() {
    return {
      title: 'Event #' + this.event.title,
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'What you need to know about event #' + this.event.id
        }
      ]
    }
  }
}
</script>
