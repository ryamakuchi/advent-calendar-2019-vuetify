<template>
  <v-layout
    column
    justify-center
    align-center
  >
    <h1>Nuxt.js Advent Calendar 2019</h1>
    <p>
      {{ comment }}
    </p>

    <v-sheet width="1200" height="auto">
      <v-calendar
        type="custom-weekly"
        start="2019-12-01"
        end="2019-12-25"
        color="info"
      >
        <template v-slot:day="{ day }">
          <v-row
            class="fill-height"
          >
            <v-sheet
              width="100%"
              height="100%"
              tile
              v-if="days[day - 1]"
            >
              <v-list-item>
                <v-list-item-avatar tile size="30">
                  <v-img
                    :src="days[day - 1].authorImageUrl"
                    :alt="days[day - 1].authorName"
                  ></v-img>
                </v-list-item-avatar>

                <a
                  :href="`https://qiita.com/${days[day - 1].authorName}`"
                  class="d-inline-block text-truncate"
                  target="_blank"
                  rel="noopener noreferrer"
                >
                  {{ days[day - 1].authorName }}
                </a>
              </v-list-item>

              <v-list-item>
                <a v-if="days[day - 1].articleUrl !== null"
                  :href="days[day - 1].articleUrl"
                  rel="noopener noreferrer"
                  class="pr-4 pl-4 pb-4"
                >
                  {{ days[day - 1].comment }}
                </a>
                <p v-else class="pr-4 pl-4 pb-4">
                  {{ days[day - 1].comment }}
                </p>
              </v-list-item>
            </v-sheet>
          </v-row>
        </template>
      </v-calendar>
    </v-sheet>

    <p class="pt-6">
      ※ このページはレスポンシブ対応していません。デスクトップサイズの画面でご覧ください。
    </p>
  </v-layout>
</template>

<script>
import { parse } from 'node-html-parser'

export default {
  async asyncData({ $axios }) {
    const { data } = await $axios.get('https://qiita.com/advent-calendar/2019/nuxt-js')
    const root = parse(data)
    const days = root.querySelectorAll('.adventCalendarCalendar_day').map(day => {
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

    return {
      comment: root.querySelector('.markdownContent').text,
      days: days
    }
  }
}
</script>
