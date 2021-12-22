<template>
  <span :title="hummanFriendlyDate">
    {{ diffForHumans }}
  </span>
</template>

<script>
import dayjs from 'dayjs'
import relativeTime from 'dayjs/plugin/relativeTime'
import localizeDate from 'dayjs/plugin/localizedFormat'
dayjs.extend(localizeDate)
dayjs.extend(relativeTime)

export default {
  props: {
    timestamp: {
      required: true,
      type: [Number, Object]
    }
  },
  computed: {
    normalizedTimestamp () {
      return this.timestamp?.seconds || this.timestamp
    },
    diffForHumans () {
      return dayjs.unix(this.normalizedTimestamp).fromNow()
    },
    hummanFriendlyDate () {
      return dayjs.unix(this.normalizedTimestamp).format('llll')
    }
  }
}
</script>

<style scoped></style>
