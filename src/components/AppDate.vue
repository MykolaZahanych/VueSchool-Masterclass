<template>
  <span :title="hummanFriendlyDate()">
    {{ diffForHumans() }}
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
      type: Number
    }
  },
  methods: {
    diffForHumans () {
      return dayjs.unix(this.timestamp).fromNow()
    },
    hummanFriendlyDate () {
      return dayjs.unix(this.timestamp).format('llll')
    }
  }
}
</script>

<style scoped></style>
