<template>
  <FullCalendar :options="calendarOptions" />
</template>

<script>

import FullCalendar from '@fullcalendar/vue3'
import dayGridPlugin from '@fullcalendar/daygrid'
import interactionPlugin from '@fullcalendar/interaction'
import timeGridPlugin from '@fullcalendar/timegrid';
import req from 'superagent'; // ajax library

export default {
  components: {
    FullCalendar // make the <FullCalendar> tag available
  },
  data() {
    return {
      calendarOptions: {
        plugins: [ timeGridPlugin, dayGridPlugin, interactionPlugin ],
        initialView: 'timeGridWeek',

        headerToolbar: {
          left: 'prev,next today',
          center: 'title',
          right: 'dayGridMonth,timeGridWeek,timeGridDay'
        },

        firstDay: 1,
        locale: 'nl',
        events: function(info, successCallback, failureCallback) {
          req.get('events.json').end((err, res) => {
            successCallback(JSON.parse(res.text));
          });
        }
      }
    }
  }
}
</script>

<style scoped>

</style>