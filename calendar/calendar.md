---
layout: calendar
title: 
permalink: /calendar/
---


<script src='https://unpkg.com/@fullcalendar/core@4.3.1/main.min.js'></script>


<link href='https://unpkg.com/@fullcalendar/core@4.3.1/main.min.css' rel='stylesheet' />
<link href='https://unpkg.com/@fullcalendar/daygrid@4.3.0/main.min.css' rel='stylesheet' />
<link href='https://unpkg.com/@fullcalendar/list@4.3.0/main.min.css' rel='stylesheet' />

<script src='https://unpkg.com/@fullcalendar/daygrid@4.3.0/main.min.js'></script>
<script src='https://unpkg.com/@fullcalendar/list@4.3.0/main.min.js'></script>
<script src='https://unpkg.com/@fullcalendar/google-calendar@4.3.0/main.min.js'></script>

<style>

#calendarContainer {
  width: 800px;
  height: 450px;
}

.fc-scroller {
  height: auto !important;
}

.fc-head .fc-widget-header {
  margin-right: 0 !important;
}

.fc-scroller {
  overflow: visible !important;
}

.fc-today {
    background: #FFF !important;
    border: none !important;
    border-top: 1px solid #ddd !important;
    font-weight: bold;
} 
</style>

  <script>

  document.addEventListener('DOMContentLoaded', function() {
    var calendarEl = document.getElementById('calendar');

    var calendar = new FullCalendar.Calendar(calendarEl, {
      plugins: [ 'dayGrid', 'googleCalendar' ],
      header: {
        left: 'prev',
        center: 'title',
        right: 'next today' 
      },
      firstDay: 1,
      hiddenDays: [0,6],
      

      displayEventTime: false, // don't show the time column in list view
      googleCalendarApiKey: 'AIzaSyCcN07bgoXITC7FBY7mq5mnYVR05fIUh9k',
      events: 'cf96q2jcqhgh2jh5rt0rc49jns@group.calendar.google.com',
      eventColor: '#808080',
      eventTextColor: '#FFFFFF',

      eventClick: function(arg) {

        // opens events in a popup window
        window.open(arg.event.url, '_blank', 'width=700,height=600');

        // prevents current tab from navigating
        arg.jsEvent.preventDefault();
      }

    });

    calendar.render();
  });

</script>


<div id="calendarContainer">
  <div id="calendar"></div>
</div>
