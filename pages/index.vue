<template>
  <v-layout
    column
    justify-center
    align-center
  >
    <pre>
      {{ comment }}
      {{ dayNames }}
    </pre>
  </v-layout>
</template>

<script>
import { parse } from 'node-html-parser'

export default {
  async asyncData({ $axios }) {
    const { data } = await $axios.get('https://qiita.com/advent-calendar/2019/nuxt-js')
    const root = parse(data)
    return {
      comment: root.querySelector('.markdownContent').text,
      dayNames: root.querySelectorAll('.adventCalendarCalendar_dayName').map(dayName => dayName.text),
      days: root.querySelectorAll('.adventCalendarCalendar_day').map(day => {
        const articleUrl = day.querySelector('.adventCalendarCalendar_comment').querySelector('a') ?
          day.querySelector('.adventCalendarCalendar_comment').querySelector('a').attributes['href'] :
          null
        return {
          date: day.querySelector('.adventCalendarCalendar_date').text,
          authorName: day.querySelector('.adventCalendarCalendar_author').text.replace(/\s|&nbsp;/g, ''),
          authorImageUrl: day.querySelector('.adventCalendarCalendar_authorIcon').attributes['src'],
          comment: day.querySelector('.adventCalendarCalendar_comment').text,
          articleUrl: articleUrl
        }
      })
    }
  }
}
</script>
