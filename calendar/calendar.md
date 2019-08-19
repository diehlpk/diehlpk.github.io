---
layout: page
title: 
permalink: /calendar/
type: info
header_text: Queen's Sailing Calendar
calendar: true
---

<script src='{{ base.url | prepend: site.url }}/js/fullcalendar/core/main.js'></script>
<script src='{{ base.url | prepend: site.url }}/js/fullcalendar/google-calendar/main.js'></script>


<script >

  document.addEventListener('DOMContentLoaded', function() {
    var calendarEl = document.getElementById('calendar');

    var calendar = new FullCalendar.Calendar(calendarEl, {
      googleCalendarApiKey: 'AIzaSyBk73GPT-mq1sEpFuI2edDSgyI9G47eod4',
      eventSources: [
        {
          googleCalendarId: 'cf96q2jcqhgh2jh5rt0rc49jns@group.calendar.google.com'
        }
      ]
    });

    calendar.render();
  });

</script>