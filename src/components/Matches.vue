<template>
  <div class="matches">
    <FullCalendar :options="calendarOptions" />  </div>
</template>

<script>
import '@fullcalendar/core/vdom' // solves problem with Vite
import FullCalendar from '@fullcalendar/vue'
import dayGridPlugin from '@fullcalendar/daygrid'
import interactionPlugin from '@fullcalendar/interaction'
import listPlugin from '@fullcalendar/list';
import Tooltip from "tooltip.js";

export default {
  name: 'Matches',
  components: {
    FullCalendar // make the <FullCalendar> tag available
  },
  data() {
    return {
      calendarOptions: {
        plugins: [dayGridPlugin, interactionPlugin, listPlugin],
        initialView: 'dayGridMonth',
        weekends: false,
        headerToolbar: {
          left: 'prev,next today',
          center: 'title',
          right: 'dayGridMonth,dayGridWeek,listMonth'
        },
        eventDidMount: function (info) {
          // Tooltip on hoover
          var tooltip = new Tooltip(info.el, {
            title: info.event.title + ' vs ' + info.event.extendedProps.Opposition +
                ' (' + info.event.extendedProps.HomeAway + ')',
            placement: 'top',
            trigger: 'hover',
            container: 'body'
          });
          console.log(tooltip)

          // Add the extra fields to display
          let title = info.el.getElementsByClassName('fc-event-title')[0]
          if (title) {
            // If grid view, add in the opposition
            title.append(" v " + info.event.extendedProps.Opposition)
          } else {
            // If list view, add in the home away and the location
            let titlelist = info.el.getElementsByClassName('fc-list-event-title')[0]
            if (titlelist) {
              titlelist.append(" vs " + info.event.extendedProps.Opposition +
                  " (" + info.event.extendedProps.HomeAway + ") " +
                  info.event.extendedProps.Location)
            }
          }

          // Colour the Away games red
          if (info.event.extendedProps.HomeAway === 'Away') {

            // Change color of dot marker
            let dotEl = info.el.getElementsByClassName('fc-daygrid-event-dot')[0];
            if (dotEl) {
              dotEl.style.borderColor = 'red';
            } else {
              let dotELlist = info.el.getElementsByClassName('fc-list-event-dot')[0];
              if (dotELlist) {
                dotELlist.style.borderColor = 'red';
              }
            }
          }
        },
        events: [
          {
            "title": "Playford Trophy",
            "Opposition": "Glevering",
            "HomeAway": "Away",
            "Location": "Glevering Hall",
            "start": "2022-12-16T19:00:00"
          },
          {
            "title": "Ladies A",
            "Division": 1,
            "Opposition": "Belstead & Bergholt",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, The Street, Rushmere",
            "start": "2022-09-28T20:00:00"
          },
          {
            "title": "Ladies A",
            "Division": 1,
            "Opposition": "Stowmarket",
            "HomeAway": "Away",
            "Location": "Mid Suffolk Leisure Centre",
            "start": "2022-10-17T20:00:00"
          },
          {
            "title": "Ladies A",
            "Division": 1,
            "Opposition": "Corinthians A",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, The Street, Rushmere",
            "start": "2022-11-02T20:00:00"
          },
          {
            "title": "Ladies A",
            "Division": 1,
            "Opposition": "Abbeygate",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, The Street, Rushmere",
            "start": "2022-11-16T20:00:00"
          },
          {
            "title": "Ladies A",
            "Division": 1,
            "Opposition": "Glevering",
            "HomeAway": "Away",
            "Location": "Glevering Hall",
            "start": "2022-11-29T19:00:00"
          },
          {
            "title": "Ladies A",
            "Division": 1,
            "Opposition": "YMCA",
            "HomeAway": "Away",
            "Location": "Suffolk One",
            "start": "2023-01-04T19:00:00"
          },
          {
            "title": "Ladies A",
            "Division": 1,
            "Opposition": "Glevering",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, The Street, Rushmere",
            "start": "2023-01-18T20:00:00"
          },
          {
            "title": "Ladies A",
            "Division": 1,
            "Opposition": "Corinthians A",
            "HomeAway": "Away",
            "Location": "Ipswich School Sports Hall",
            "start": "2023-01-31T20:15:00"
          },
          {
            "title": "Ladies A",
            "Division": 1,
            "Opposition": "Abbeygate",
            "HomeAway": "Away",
            "Location": "King Edward VI School, Bury St Edmunds",
            "start": "2023-02-08T19:00:00"
          },
          {
            "title": "Ladies A",
            "Division": 1,
            "Opposition": "YMCA",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, The Street, Rushmere",
            "start": "2023-02-22T20:00:00"
          },
          {
            "title": "Ladies A",
            "Division": 1,
            "Opposition": "Belstead & Bergholt",
            "HomeAway": "Away",
            "Location": "Goals, Suffolk New College",
            "start": "2023-02-27T20:00:00"
          },
          {
            "title": "Ladies A",
            "Division": 1,
            "Opposition": "Stowmarket",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, The Street, Rushmere",
            "start": "2023-03-08T20:00:00"
          },
          {
            "title": "Ladies B",
            "Division": 2,
            "Opposition": "Felixstowe",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, The Street, Rushmere",
            "start": "2022-10-19T20:00:00"
          },
          {
            "title": "Ladies B",
            "Division": 2,
            "Opposition": "Needham",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, The Street, Rushmere",
            "start": "2023-03-01T20:00:00"
          },
          {
            "title": "Ladies B",
            "Division": 2,
            "Opposition": "Skillcentre",
            "HomeAway": "Away",
            "Location": "Handford Hall School",
            "start": "2022-11-03T19:15:00"
          },
          {
            "title": "Ladies B",
            "Division": 2,
            "Opposition": "DVE",
            "HomeAway": "Away",
            "Location": "Debenham Sports and Leisure Centre",
            "start": "2022-11-18T20:15:00"
          },
          {
            "title": "Ladies B",
            "Division": 2,
            "Opposition": "Corinthians B",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, The Street, Rushmere",
            "start": "2022-11-30T20:00:00"
          },
          {
            "title": "Ladies B",
            "Division": 2,
            "Opposition": "Felixstowe",
            "HomeAway": "Away",
            "Location": "Brackenbury Sports Centre",
            "start": "2023-01-09T19:00:00"
          },
          {
            "title": "Ladies B",
            "Division": 2,
            "Opposition": "Needham",
            "HomeAway": "Away",
            "Location": "Mid Suffolk Leisure Centre, Stowmarket",
            "start": "2023-02-02T20:00:00"
          },
          {
            "title": "Ladies B",
            "Division": 2,
            "Opposition": "DVE",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, The Street, Rushmere",
            "start": "2023-02-15T20:00:00"
          },
          {
            "title": "Ladies B",
            "Division": 2,
            "Opposition": "Corinthians B",
            "HomeAway": "Away",
            "Location": "Ipswich School Sports Hall",
            "start": "2023-03-07T20:15:00"
          },
          {
            "title": "Ladies B",
            "Division": 2,
            "Opposition": "Skillcentre",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, The Street, Rushmere",
            "start": "2023-03-20T20:00:00"
          },
          {
            "title": "Mens A",
            "Division": 1,
            "Opposition": "Belstead & Bergholt",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, The Street, Rushmere",
            "start": "2022-09-28T20:00:00"
          },
          {
            "title": "Mens A",
            "Division": 1,
            "Opposition": "Thorpeness",
            "HomeAway": "Away",
            "Location": "Wickham Market Primary School",
            "start": "2022-10-07T19:00:00"
          },
          {
            "title": "Mens A",
            "Division": 1,
            "Opposition": "Stowmarket A",
            "HomeAway": "Away",
            "Location": "Mid Suffolk Leisure Centre",
            "start": "2022-10-17T20:00:00"
          },
          {
            "title": "Mens A",
            "Division": 1,
            "Opposition": "YMCA A",
            "HomeAway": "Away",
            "Location": "Suffolk One",
            "start": "2022-10-26T19:00:00"
          },
          {
            "title": "Mens A",
            "Division": 1,
            "Opposition": "Corinthians A",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, The Street, Rushmere",
            "start": "2022-11-02T20:00:00"
          },
          {
            "title": "Mens A",
            "Division": 1,
            "Opposition": "Abbeygate A",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, The Street, Rushmere",
            "start": "2022-11-16T20:00:00"
          },
          {
            "title": "Mens A",
            "Division": 1,
            "Opposition": "Thorpeness",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, The Street, Rushmere",
            "start": "2022-12-07T20:00:00"
          },
          {
            "title": "Mens A",
            "Division": 1,
            "Opposition": "Belstead & Bergholt",
            "HomeAway": "Away",
            "Location": "Goals, Suffolk New College",
            "start": "2023-01-09T20:00:00"
          },
          {
            "title": "Mens A",
            "Division": 1,
            "Opposition": "Corinthians A",
            "HomeAway": "Away",
            "Location": "Ipswich School Sports Hall",
            "start": "2023-01-31T20:15:00"
          },
          {
            "title": "Mens A",
            "Division": 1,
            "Opposition": "Abbeygate A",
            "HomeAway": "Away",
            "Location": "King Edward VI School, Bury St Edmunds",
            "start": "2023-02-08T19:00:00"
          },
          {
            "title": "Mens A",
            "Division": 1,
            "Opposition": "YMCA A",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, The Street, Rushmere",
            "start": "2023-02-22T20:00:00"
          },
          {
            "title": "Mens A",
            "Division": 1,
            "Opposition": "Stowmarket A",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, The Street, Rushmere",
            "start": "2023-03-08T20:00:00"
          },
          {
            "title": "Mens B",
            "Division": 2,
            "Opposition": "DVE A",
            "HomeAway": "Away",
            "Location": "Debenham Sports and Leisure Centre",
            "start": "2022-10-07T20:15:00"
          },
          {
            "title": "Mens B",
            "Division": 2,
            "Opposition": "YMCA B",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, The Street, Rushmere",
            "start": "2022-10-19T20:00:00"
          },
          {
            "title": "Mens B",
            "Division": 2,
            "Opposition": "Needham",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, The Street, Rushmere",
            "start": "2022-10-26T20:00:00"
          },
          {
            "title": "Mens B",
            "Division": 2,
            "Opposition": "Glevering A",
            "HomeAway": "Away",
            "Location": "Glevering Hall",
            "start": "2022-11-08T19:00:00"
          },
          {
            "title": "Mens B",
            "Division": 2,
            "Opposition": "Felixstowe A",
            "HomeAway": "Away",
            "Location": "Brackenbury Sports Centre",
            "start": "2022-11-14T19:00:00"
          },
          {
            "title": "Mens B",
            "Division": 2,
            "Opposition": "Corinthians B",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, The Street, Rushmere",
            "start": "2022-11-30T20:00:00"
          },
          {
            "title": "Mens B",
            "Division": 2,
            "Opposition": "DVE A",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, The Street, Rushmere",
            "start": "2023-01-04T20:00:00"
          },
          {
            "title": "Mens B",
            "Division": 2,
            "Opposition": "Glevering A",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, The Street, Rushmere",
            "start": "2023-01-18T20:00:00"
          },
          {
            "title": "Mens B",
            "Division": 2,
            "Opposition": "Needham",
            "HomeAway": "Away",
            "Location": "Mid Suffolk Leisure Centre, Stowmarket",
            "start": "2023-01-24T20:00:00"
          },
          {
            "title": "Mens B",
            "Division": 2,
            "Opposition": "YMCA B",
            "HomeAway": "Away",
            "Location": "Suffolk One",
            "start": "2023-02-08T19:00:00"
          },
          {
            "title": "Mens B",
            "Division": 2,
            "Opposition": "Corinthians B",
            "HomeAway": "Away",
            "Location": "Ipswich School Sports Hall",
            "start": "2023-03-07T20:15:00"
          },
          {
            "title": "Mens B",
            "Division": 2,
            "Opposition": "Felixstowe A",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, The Street, Rushmere",
            "start": "2023-03-22T20:00:00"
          },
          {
            "title": "Mens C",
            "Division": 3,
            "Opposition": "DVE B",
            "HomeAway": "Away",
            "Location": "Debenham Sports and Leisure Centre",
            "start": "2022-09-23T20:15:00"
          },
          {
            "title": "Mens C",
            "Division": 3,
            "Opposition": "Rushmere D",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, The Street, Rushmere",
            "start": "2022-10-05T20:00:00"
          },
          {
            "title": "Mens C",
            "Division": 3,
            "Opposition": "Corinthians C",
            "HomeAway": "Away",
            "Location": "Ipswich School Sports Hall",
            "start": "2022-10-18T20:15:00"
          },
          {
            "title": "Mens C",
            "Division": 3,
            "Opposition": "Rushmere D",
            "HomeAway": "Away",
            "Location": "Ipswich School Sports Centre, The Street, Rushmere",
            "start": "2022-11-23T20:00:00"
          },
          {
            "title": "Mens C",
            "Division": 3,
            "Opposition": "Woodbridge A",
            "HomeAway": "Away",
            "Location": "Kesgrave High School",
            "start": "2022-12-01T19:30:00"
          },
          {
            "title": "Mens C",
            "Division": 3,
            "Opposition": "DVE B",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, The Street, Rushmere",
            "start": "2023-01-04T20:00:00"
          },
          {
            "title": "Mens C",
            "Division": 3,
            "Opposition": "Woodbridge A",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, The Street, Rushmere",
            "start": "2023-01-11T20:00:00"
          },
          {
            "title": "Mens C",
            "Division": 3,
            "Opposition": "Abbeygate B",
            "HomeAway": "Away",
            "Location": "King Edward VI School, Bury St Edmunds",
            "start": "2023-01-25T19:00:00"
          },
          {
            "title": "Mens C",
            "Division": 3,
            "Opposition": "Corinthians C",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, The Street, Rushmere",
            "start": "2023-02-01T20:00:00"
          },
          {
            "title": "Mens C",
            "Division": 3,
            "Opposition": "Abbeygate B",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, The Street, Rushmere",
            "start": "2023-03-29T20:00:00"
          },
          {
            "title": "Mens D",
            "Division": 3,
            "Opposition": "Corinthians C",
            "HomeAway": "Away",
            "Location": "Ipswich School Sports Hall",
            "start": "2023-02-09T19:30:00"
          },
          {
            "title": "Mens D",
            "Division": 3,
            "Opposition": "Rushmere C",
            "HomeAway": "Away",
            "Location": "Ipswich School Sports Centre, The Street, Rushmere",
            "start": "2022-10-05T20:00:00"
          },
          {
            "title": "Mens D",
            "Division": 3,
            "Opposition": "Woodbridge A",
            "HomeAway": "Away",
            "Location": "Kesgrave High School",
            "start": "2022-10-13T19:30:00"
          },
          {
            "title": "Mens D",
            "Division": 3,
            "Opposition": "DVE B",
            "HomeAway": "Away",
            "Location": "Debenham Sports and Leisure Centre",
            "start": "2022-10-21T20:15:00"
          },
          {
            "title": "Mens D",
            "Division": 3,
            "Opposition": "Abbeygate B",
            "HomeAway": "Away",
            "Location": "King Edward VI School, Bury St Edmunds",
            "start": "2022-11-16T19:00:00"
          },
          {
            "title": "Mens D",
            "Division": 3,
            "Opposition": "Rushmere C",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, The Street, Rushmere",
            "start": "2022-11-23T20:00:00"
          },
          {
            "title": "Mens D",
            "Division": 3,
            "Opposition": "Abbeygate B",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, The Street, Rushmere",
            "start": "2023-01-11T20:00:00"
          },
          {
            "title": "Mens D",
            "Division": 3,
            "Opposition": "Woodbridge A",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, The Street, Rushmere",
            "start": "2023-02-01T20:00:00"
          },
          {
            "title": "Mens D",
            "Division": 3,
            "Opposition": "Corinthians C",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, The Street, Rushmere",
            "start": "2023-02-15T20:00:00"
          },
          {
            "title": "Mens D",
            "Division": 3,
            "Opposition": "DVE B",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, The Street, Rushmere",
            "start": "2023-03-01T20:00:00"
          },
          {
            "title": "Mixed A",
            "Division": 1,
            "Opposition": "YMCA A",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, The Street, Rushmere",
            "start": "2022-10-12T20:00:00"
          },
          {
            "title": "Mixed A",
            "Division": 1,
            "Opposition": "Stowmarket A",
            "HomeAway": "Away",
            "Location": "Mid Suffolk Leisure Centre",
            "start": "2022-11-21T20:00:00"
          },
          {
            "title": "Mixed A",
            "Division": 1,
            "Opposition": "Corinthians A",
            "HomeAway": "Away",
            "Location": "Ipswich School Sports Hall",
            "start": "2022-12-06T20:15:00"
          },
          {
            "title": "Mixed A",
            "Division": 1,
            "Opposition": "Belstead & Bergholt A",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, The Street, Rushmere",
            "start": "2022-12-14T20:00:00"
          },
          {
            "title": "Mixed A",
            "Division": 1,
            "Opposition": "Corinthians B",
            "HomeAway": "Away",
            "Location": "Ipswich School Sports Hall",
            "start": "2022-12-20T20:15:00"
          },
          {
            "title": "Mixed A",
            "Division": 1,
            "Opposition": "Corinthians B",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, The Street, Rushmere",
            "start": "2023-01-25T20:00:00"
          },
          {
            "title": "Mixed A",
            "Division": 1,
            "Opposition": "Abbeygate A",
            "HomeAway": "Away",
            "Location": "King Edward VI School, Bury St Edmunds",
            "start": "2023-02-06T19:00:00"
          },
          {
            "title": "Mixed A",
            "Division": 1,
            "Opposition": "YMCA A",
            "HomeAway": "Away",
            "Location": "Suffolk One",
            "start": "2023-02-15T19:00:00"
          },
          {
            "title": "Mixed A",
            "Division": 1,
            "Opposition": "Belstead & Bergholt A",
            "HomeAway": "Away",
            "Location": "Goals, Suffolk New College",
            "start": "2023-02-20T20:00:00"
          },
          {
            "title": "Mixed A",
            "Division": 1,
            "Opposition": "Stowmarket A",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, The Street, Rushmere",
            "start": "2023-03-15T20:00:00"
          },
          {
            "title": "Mixed A",
            "Division": 1,
            "Opposition": "Corinitians A",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, The Street, Rushmere",
            "start": "2023-03-22T20:00:00"
          },
          {
            "title": "Mixed A",
            "Division": 1,
            "Opposition": "Abbeygate A",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, The Street, Rushmere",
            "start": "2023-03-29T20:00:00"
          },
          {
            "title": "Mixed B",
            "Division": 3,
            "Opposition": "Framlingham A",
            "HomeAway": "Away",
            "Location": "Thomas Mills High School Sports Centre",
            "start": "2022-09-23T20:00:00"
          },
          {
            "title": "Mixed B",
            "Division": 3,
            "Opposition": "Belstead & Bergholt B",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, The Street, Rushmere",
            "start": "2022-10-05T20:00:00"
          },
          {
            "title": "Mixed B",
            "Division": 3,
            "Opposition": "Stowmarket B",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, The Street, Rushmere",
            "start": "2022-10-12T20:00:00"
          },
          {
            "title": "Mixed B",
            "Division": 3,
            "Opposition": "Felixstowe B",
            "HomeAway": "Away",
            "Location": "Brackenbury Sports Centre",
            "start": "2022-10-31T19:00:00"
          },
          {
            "title": "Mixed B",
            "Division": 3,
            "Opposition": "Skillcentre A",
            "HomeAway": "Away",
            "Location": "Handford Hall School",
            "start": "2022-11-10T19:15:00"
          },
          {
            "title": "Mixed B",
            "Division": 3,
            "Opposition": "DVE",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, The Street, Rushmere",
            "start": "2022-11-23T20:00:00"
          },
          {
            "title": "Mixed B",
            "Division": 3,
            "Opposition": "Framlingham A",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, The Street, Rushmere",
            "start": "2022-12-07T20:00:00"
          },
          {
            "title": "Mixed B",
            "Division": 3,
            "Opposition": "Skillcentre A",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, The Street, Rushmere",
            "start": "2022-12-14T20:00:00"
          },
          {
            "title": "Mixed B",
            "Division": 3,
            "Opposition": "Corinthians D",
            "HomeAway": "Away",
            "Location": "Ipswich School Sports Hall",
            "start": "2022-12-20T20:15:00"
          },
          {
            "title": "Mixed B",
            "Division": 3,
            "Opposition": "DVE",
            "HomeAway": "Away",
            "Location": "Debenham Sports and Leisure Centre",
            "start": "2023-01-06T20:15:00"
          },
          {
            "title": "Mixed B",
            "Division": 3,
            "Opposition": "Stowmarket B",
            "HomeAway": "Away",
            "Location": "Mid Suffolk Leisure Centre",
            "start": "2023-01-16T20:00:00"
          },
          {
            "title": "Mixed B",
            "Division": 3,
            "Opposition": "Corinthians D",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, The Street, Rushmere",
            "start": "2023-01-25T20:00:00"
          },
          {
            "title": "Mixed B",
            "Division": 3,
            "Opposition": "Felixstowe B",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, The Street, Rushmere",
            "start": "2023-03-15T20:00:00"
          },
          {
            "title": "Mixed B",
            "Division": 3,
            "Opposition": "Belstead & Bergholt B",
            "HomeAway": "Away",
            "Location": "Goals, Suffolk New College",
            "start": "2023-03-27T20:00:00"
          }
        ]
      }
    }
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

.popper,
.tooltip {
  position: absolute;
  z-index: 9999;
  background: #FFC107;
  color: black;
  width: 250px;
  border-radius: 3px;
  box-shadow: 0 0 2px rgba(0,0,0,0.5);
  padding: 5px;
  text-align: center;
}

</style>
