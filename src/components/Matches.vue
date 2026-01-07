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
            "Opposition": "Skillcentre",
            "HomeAway": "Away",
            "Location": "Handford Hall School",
            "start": "2023-10-09T19:15:00"
          },
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
            "start": "2023-02-20T20:00:00"
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
            "start": "2023-04-27T19:30:00"
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
            "start": "2023-04-04T20:15:00"
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
          },
          {"title": "Ladies A,","Division": "L1","Opposition": "Rushmere","HomeAway":"Away","Location": "Ipswich School Sports Centre, The Street, Rusmere","start": "2023-09-18T20:00:00"},
          {"title": "Ladies B,","Division": "L1","Opposition": "Rushmere","HomeAway":"Home","Location": "Ipswich School Sports Centre, The Street, Rushmere","start": "2023-09-18T20:00:00"},
          {"title": "Men's D,","Division": "M4","Opposition": "Ipswich Tigers","HomeAway":"Away","Location": "Inspire Suffolk, Lindbergh Road, Ipswich","start": "2023-09-25T20:00:00"},
          {"title": "Mixed B,","Division": "Mx2","Opposition": "Thorpeness","HomeAway":"Home","Location": "Ipswich School Sports Centre, The Street, Rushmere","start": "2023-09-25T20:00:00"},
          {"title": "Ladies A,","Division": "L1","Opposition": "Ipswich YM Exiles","HomeAway":"Away","Location": "Suffolk One, Scrivener Drive, Ipswich","start": "2024-04-10T19:00:00"},
          {"title": "Men's A,","Division": "M1","Opposition": "Ipswich YM Exiles","HomeAway":"Away","Location": "Suffolk One, Scrivener Drive, Ipswich","start": "2023-09-27T19:00:00"},
          {"title": "Mixed B,","Division": "Mx2","Opposition": "Belstead Belstead & Bergholt} Bergholt","HomeAway":"Away","Location": "Goals, Suffolk New College","start": "2023-10-02T20:00:00"},
          {"title": "Ladies B,","Division": "L1","Opposition": "Corinthians","HomeAway":"Away","Location": "Ipswich School Sports Hall","start": "2023-10-03T20:30:00"},
          {"title": "Men's D,","Division": "M4","Opposition": "Stradbroke","HomeAway":"Away","Location": "Hartismere High School, Castleton Way, Eye","start": "2023-10-03T19:00:00"},
          {"title": "Men's B,","Division": "M2","Opposition": "Corinthians A","HomeAway":"Home","Location": "Ipswich School Sports Centre, The Street, Rushmere","start": "2023-10-04T20:00:00"},
          {"title": "Men's C,","Division": "M3","Opposition": "Corinthians","HomeAway":"Home","Location": "Ipswich School Sports Centre, The Street, Rushmere","start": "2023-10-04T20:00:00"},
          {"title": "Men's A,","Division": "M1","Opposition": "Abbeygate","HomeAway":"Away","Location": "King Edward VI School, Bury St Edmunds","start": "2023-10-11T19:00:00"},
          {"title": "Men's C,","Division": "M3","Opposition": "Abbeygate","HomeAway":"Away","Location": "King Edward VI School, Bury St Edmunds","start": "2023-10-11T19:00:00"},
          {"title": "Mixed C","Division": "Mx5","Opposition": "DVE","HomeAway":"Away","Location": "Debenham Sports and Leisure Centre","start": "2024-01-26T20:15:00"},
          {"title": "Ladies A,","Division": "L1","Opposition": "Rushmere","HomeAway":"Home","Location": "Ipswich School Sports Centre, The Street, Rushmere","start": "2023-10-16T20:00:00"},
          {"title": "Ladies B,","Division": "L1","Opposition": "Rushmere","HomeAway":"Away","Location": "Ipswich School Sports Centre, The Street, Rusmere","start": "2023-10-16T20:00:00"},
          {"title": "Men's C,","Division": "M3","Opposition": "Ipswich Tigers","HomeAway":"Home","Location": "Ipswich School Sports Centre, The Street, Rushmere","start": "2023-10-18T20:00:00"},
          {"title": "Mixed A,","Division": "Mx1","Opposition": "Corinthians","HomeAway":"Home","Location": "Ipswich School Sports Centre, The Street, Rushmere","start": "2023-10-18T20:00:00"},
          {"title": "Men's D,","Division": "M4","Opposition": "Framlingham","HomeAway":"Away","Location": "Thomas Mills High School Sports Centre","start": "2023-10-20T20:00:00"},
          {"title": "Men's B,","Division": "M2","Opposition": "Corinthians B","HomeAway":"Away","Location": "Ipswich School Sports Hall","start": "2023-10-24T20:30:00"},
          {"title": "Men's D,","Division": "M4","Opposition": "Corinthians","HomeAway":"Away","Location": "Ipswich School Sports Hall","start": "2023-10-24T20:30:00"},
          {"title": "Ladies A,","Division": "L1","Opposition": "Abbeygate","HomeAway":"Home","Location": "Ipswich School Sports Centre, The Street, Rushmere","start": "2023-10-25T20:00:00"},
          {"title": "Men's A,","Division": "M1","Opposition": "Belstead Belstead & Bergholt} Bergholt","HomeAway":"Home","Location": "Ipswich School Sports Centre, The Street, Rushmere","start": "2023-10-25T20:00:00"},
          {"title": "Ladies B,","Division": "L1","Opposition": "Stowmarket","HomeAway":"Away","Location": "Mid Suffolk Leisure Centre","start": "2023-10-30T20:00:00"},
          {"title": "Men's D,","Division": "M4","Opposition": "Stowmarket","HomeAway":"Away","Location": "Mid Suffolk Leisure Centre","start": "2023-10-30T20:00:00"},
          {"title": "Ladies A,","Division": "L1","Opposition": "Corinthians","HomeAway":"Home","Location": "Ipswich School Sports Centre, The Street, Rushmere","start": "2023-11-01T20:00:00"},
          {"title": "Men's A,","Division": "M1","Opposition": "DVE","HomeAway":"Home","Location": "Ipswich School Sports Centre, The Street, Rushmere","start": "2023-11-01T20:00:00"},
          {"title": "Mixed C,","Division": "Mx5","Opposition": "Thorpeness","HomeAway":"Away","Location": "Wickham Market Primary School","start": "2023-11-03T19:00:00"},
          {"title": "Mixed A,","Division": "Mx1","Opposition": "Abbeygate","HomeAway":"Away","Location": "King Edward VI School, Bury St Edmunds","start": "2023-11-06T19:00:00"},
          {"title": "Mixed B,","Division": "Mx2","Opposition": "Corinthians","HomeAway":"Away","Location": "Ipswich School Sports Hall","start": "2023-11-07T20:30:00"},
          {"title": "Men's B,","Division": "M2","Opposition": "Needham","HomeAway":"Away","Location": "Mid Suffolk Leisure Centre, Stowmarket","start": "2023-11-09T20:00:00"},
          {"title": "Mixed B,","Division": "Mx2","Opposition": "Abbeygate","HomeAway":"Home","Location": "Ipswich School Sports Centre, The Street, Rushmere","start": "2023-11-13T20:00:00"},
          {"title": "Ladies B,","Division": "L1","Opposition": "Belstead Belstead & Bergholt} Bergholt","HomeAway":"Home","Location": "Ipswich School Sports Centre, The Street, Rushmere","start": "2023-11-15T20:00:00"},
          {"title": "Men's C,","Division": "M3","Opposition": "BSP Drakes","HomeAway":"Home","Location": "Ipswich School Sports Centre, The Street, Rushmere","start": "2023-11-15T20:00:00"},
          {"title": "Mixed A,","Division": "Mx1","Opposition": "Ipswich YM Exiles","HomeAway":"Away","Location": "Suffolk One, Scrivener Drive, Ipswich","start": "2023-11-15T19:00:00"},
          {"title": "Men's B,","Division": "M2","Opposition": "DVE","HomeAway":"Away","Location": "Debenham Sports and Leisure Centre","start": "2023-11-17T20:15:00"},
          {"title": "Mixed A,","Division": "Mx1","Opposition": "Belstead Belstead & Bergholt} Bergholt","HomeAway":"Away","Location": "Goals, Suffolk New College","start": "2023-11-20T20:00:00"},
          {"title": "Mixed C,","Division": "Mx5","Opposition": "Woodbridge","HomeAway":"Home","Location": "Ipswich School Sports Centre, The Street, Rushmere","start": "2023-11-20T20:00:00"},
          {"title": "Men's C,","Division": "M3","Opposition": "Abbeygate","HomeAway":"Home","Location": "Ipswich School Sports Centre, The Street, Rushmere","start": "2023-11-22T20:00:00"},
          {"title": "Mixed B,","Division": "Mx2","Opposition": "Leiston","HomeAway":"Home","Location": "Ipswich School Sports Centre, The Street, Rushmere","start": "2023-11-22T20:00:00"},
          {"title": "Men's A,","Division": "M1","Opposition": "Thorpeness","HomeAway":"Away","Location": "Wickham Market Primary School","start": "2023-11-24T19:00:00"},
          {"title": "Men's B,","Division": "M2","Opposition": "Felixstowe","HomeAway":"Away","Location": "Brackenbury Sports Centre","start": "2023-11-27T19:00:00"},
          {"title": "Ladies A,","Division": "L1","Opposition": "Stowmarket","HomeAway":"Home","Location": "Ipswich School Sports Centre, The Street, Rushmere","start": "2023-11-29T20:00:00"},
          {"title": "Men's A,","Division": "M1","Opposition": "Stowmarket","HomeAway":"Home","Location": "Ipswich School Sports Centre, The Street, Rushmere","start": "2023-11-29T20:00:00"},
          {"title": "Mixed B,","Division": "Mx2","Opposition": "Thorpeness","HomeAway":"Away","Location": "Wickham Market Primary School","start": "2023-12-01T19:00:00"},
          {"title": "Ladies B,","Division": "L1","Opposition": "Ipswich YM Exiles","HomeAway":"Home","Location": "Ipswich School Sports Centre, The Street, Rushmere","start": "2023-12-06T20:00:00"},
          {"title": "Men's C,","Division": "M3","Opposition": "Ipswich YM Exiles","HomeAway":"Home","Location": "Ipswich School Sports Centre, The Street, Rushmere","start": "2023-12-06T20:00:00"},
          {"title": "Mixed A,","Division": "Mx1","Opposition": "Felixstowe","HomeAway":"Away","Location": "Brackenbury Sports Centre","start": "2023-12-06T19:00:00"},
          {"title": "Mixed C,","Division": "Mx5","Opposition": "Thorpeness","HomeAway":"Home","Location": "Ipswich School Sports Centre, The Street, Rushmere","start": "2023-12-11T20:00:00"},
          {"title": "Men's D,","Division": "M4","Opposition": "Skillcentre","HomeAway":"Home","Location": "Ipswich School Sports Centre, The Street, Rushmere","start": "2024-03-11T20:00:00"},
          {"title": "Mixed B,","Division": "Mx2","Opposition": "Ipswich YM Exiles","HomeAway":"Home","Location": "Ipswich School Sports Centre, The Street, Rushmere","start": "2023-12-13T20:00:00"},
          {"title": "Mixed C,","Division": "Mx5","Opposition": "Constitutional ","HomeAway":"Away","Location": "Skyliner Sports Centre, Rougham Tower Ave","start": "2023-12-19T19:00:00"},
          {"title": "Men's B,","Division": "M2","Opposition": "Glevering","HomeAway":"Away","Location": "Glevering Hall","start": "2023-12-20T19:00:00"},
          {"title": "Men's C,","Division": "M3","Opposition": "Woodbridge","HomeAway":"Home","Location": "Ipswich School Sports Centre, The Street, Rushmere","start": "2023-12-20T20:00:00"},
          {"title": "Mixed A,","Division": "Mx1","Opposition": "Stowmarket","HomeAway":"Home","Location": "Ipswich School Sports Centre, The Street, Rushmere","start": "2023-12-20T20:00:00"},
          {"title": "Ladies A,","Division": "L1","Opposition": "Ipswich YM Exiles","HomeAway":"Home","Location": "Ipswich School Sports Centre, The Street, Rushmere","start": "2024-01-03T20:00:00"},
          {"title": "Men's A,","Division": "M1","Opposition": "Ipswich YM Exiles","HomeAway":"Home","Location": "Ipswich School Sports Centre, The Street, Rushmere","start": "2024-01-03T20:00:00"},
          {"title": "Ladies B,","Division": "L1","Opposition": "Belstead Belstead & Bergholt} Bergholt","HomeAway":"Away","Location": "Goals, Suffolk New College","start": "2024-01-08T20:00:00"},
          {"title": "Men's D,","Division": "M4","Opposition": "Skillcentre","HomeAway":"Away","Location": "Handford Hall School","start": "2024-03-28T19:15:00"},
          {"title": "Mixed B,","Division": "Mx2","Opposition": "Ipswich YM Exiles","HomeAway":"Away","Location": "Suffolk One, Scrivener Drive, Ipswich","start": "2024-01-10T19:00:00"},
          {"title": "Mixed C,","Division": "Mx5","Opposition": "Woodbridge","HomeAway":"Away","Location": "Kesgrave High School","start": "2024-01-11T19:30:00"},
          {"title": "Ladies A,","Division": "L1","Opposition": "Belstead Belstead & Bergholt} Bergholt","HomeAway":"Away","Location": "Goals, Suffolk New College","start": "2024-01-15T20:00:00"},
          {"title": "Mixed C,","Division": "Mx5","Opposition": "Constitutional ","HomeAway":"Home","Location": "Ipswich School Sports Centre, The Street, Rushmere","start": "2024-01-15T20:00:00"},
          {"title": "Mixed A,","Division": "Mx1","Opposition": "Ipswich YM Exiles","HomeAway":"Home","Location": "Ipswich School Sports Centre, The Street, Rushmere","start": "2024-01-17T20:00:00"},
          {"title": "Mixed B,","Division": "Mx2","Opposition": "Corinthians","HomeAway":"Home","Location": "Ipswich School Sports Centre, The Street, Rushmere","start": "2024-01-17T20:00:00"},
          {"title": "Men's A,","Division": "M1","Opposition": "Belstead Belstead & Bergholt} Bergholt","HomeAway":"Away","Location": "Goals, Suffolk New College","start": "2024-01-22T20:00:00"},
          {"title": "Men's B,","Division": "M2","Opposition": "Corinthians A","HomeAway":"Away","Location": "Ipswich School Sports Hall","start": "2024-01-23T20:30:00"},
          {"title": "Men's C,","Division": "M3","Opposition": "Corinthians","HomeAway":"Away","Location": "Ipswich School Sports Hall","start": "2024-01-23T20:30:00"},
          {"title": "Ladies A,","Division": "L1","Opposition": "Belstead Belstead & Bergholt} Bergholt","HomeAway":"Home","Location": "Ipswich School Sports Centre, The Street, Rushmere","start": "2024-01-24T20:00:00"},
          {"title": "Ladies Friendly","Division": "Friendly","Opposition": "DVE","HomeAway":"Home","Location": "Ipswich School Sports Centre, The Street, Rushmere","start": "2024-02-14T20:00:00"},
          {"title": "Men's C,","Division": "M3","Opposition": "Ipswich Tigers","HomeAway":"Away","Location": "Inspire Suffolk, Lindbergh Road, Ipswich","start": "2024-01-29T20:00:00"},
          {"title": "Mixed A,","Division": "Mx1","Opposition": "Stowmarket","HomeAway":"Away","Location": "Mid Suffolk Leisure Centre","start": "2024-01-29T20:00:00"},
          {"title": "Ladies B,","Division": "L1","Opposition": "Abbeygate","HomeAway":"Home","Location": "Ipswich School Sports Centre, The Street, Rushmere","start": "2024-01-31T20:00:00"},
          {"title": "Men's B,","Division": "M2","Opposition": "Needham","HomeAway":"Home","Location": "Ipswich School Sports Centre, The Street, Rushmere","start": "2024-01-31T20:00:00"},
          {"title": "Mixed B,","Division": "Mx2","Opposition": "Leiston","HomeAway":"Away","Location": "Leiston Sports Centre, Red House Lane, Leiston","start": "2024-02-01T20:00:00"},
          {"title": "Mixed A,","Division": "Mx1","Opposition": "Corinthians","HomeAway":"Away","Location": "Ipswich School Sports Hall","start": "2024-02-06T20:30:00"},
          {"title": "Men's B,","Division": "M2","Opposition": "Corinthians B","HomeAway":"Home","Location": "Ipswich School Sports Centre, The Street, Rushmere","start": "2024-02-07T20:00:00"},
          {"title": "Men's D,","Division": "M4","Opposition": "Corinthians","HomeAway":"Home","Location": "Ipswich School Sports Centre, The Street, Rushmere","start": "2024-02-07T20:00:00"},
          {"title": "Men's C,","Division": "M3","Opposition": "Woodbridge","HomeAway":"Away","Location": "Kesgrave High School","start": "2024-02-08T19:30:00"},
          {"title": "Ladies A,","Division": "L1","Opposition": "Corinthians","HomeAway":"Away","Location": "Ipswich School Sports Hall","start": "2024-02-13T20:30:00"},
          {"title": "Ladies B,","Division": "L1","Opposition": "Ipswich YM Exiles","HomeAway":"Away","Location": "Suffolk One, Scrivener Drive, Ipswich","start": "2024-04-03T19:00:00"},
          {"title": "Men's B,","Division": "M2","Opposition": "DVE","HomeAway":"Home","Location": "Ipswich School Sports Centre, The Street, Rushmere","start": "2024-02-14T20:00:00"},
          {"title": "Men's C,","Division": "M3","Opposition": "Ipswich YM Exiles","HomeAway":"Away","Location": "Suffolk One, Scrivener Drive, Ipswich","start": "2024-04-03T19:00:00"},
          {"title": "Men's D,","Division": "M4","Opposition": "Ipswich Tigers","HomeAway":"Home","Location": "Ipswich School Sports Centre, The Street, Rushmere","start": "2023-11-27T20:00:00"},
          {"title": "Men's A,","Division": "M1","Opposition": "DVE","HomeAway":"Away","Location": "Debenham Sports and Leisure Centre","start": "2024-02-16T20:15:00"},
          {"title": "Mixed A,","Division": "Mx1","Opposition": "Belstead Belstead & Bergholt} Bergholt","HomeAway":"Home","Location": "Ipswich School Sports Centre, The Street, Rushmere","start": "2024-02-19T20:00:00"},
          {"title": "Men's A,","Division": "M1","Opposition": "Abbeygate","HomeAway":"Home","Location": "Ipswich School Sports Centre, The Street, Rushmere","start": "2024-02-21T20:00:00"},
          {"title": "Mixed C,","Division": "Mx5","Opposition": "DVE","HomeAway":"Home","Location": "Ipswich School Sports Centre, The Street, Rushmere","start": "2024-02-21T20:00:00"},
          {"title": "Mixed B,","Division": "Mx2","Opposition": "Abbeygate","HomeAway":"Away","Location": "King Edward VI School, Bury St Edmunds","start": "2024-02-26T19:00:00"},
          {"title": "Ladies B,","Division": "L1","Opposition": "Corinthians","HomeAway":"Home","Location": "Ipswich School Sports Centre, The Street, Rushmere","start": "2024-02-28T20:00:00"},
          {"title": "Men's C,","Division": "M3","Opposition": "BSP Drakes","HomeAway":"Away","Location": "Ipswich School Sports Hall","start": "2024-02-28T20:00:00"},
          {"title": "Mixed A,","Division": "Mx1","Opposition": "Abbeygate","HomeAway":"Home","Location": "Ipswich School Sports Centre, The Street, Rushmere","start": "2024-02-28T20:00:00"},
          {"title": "Ladies A,","Division": "L1","Opposition": "Abbeygate","HomeAway":"Away","Location": "King Edward VI School, Bury St Edmunds","start": "2024-03-04T19:00:00"},
          {"title": "Men's D,","Division": "M4","Opposition": "Stradbroke","HomeAway":"Home","Location": "Ipswich School Sports Centre, The Street, Rushmere","start": "2024-03-06T20:00:00"},
          {"title": "Mixed B,","Division": "Mx2","Opposition": "Belstead Belstead & Bergholt} Bergholt","HomeAway":"Home","Location": "Ipswich School Sports Centre, The Street, Rushmere","start": "2024-03-06T20:00:00"},
          {"title": "Ladies B,","Division": "L1","Opposition": "Abbeygate","HomeAway":"Away","Location": "King Edward VI School, Bury St Edmunds","start": "2024-03-11T19:00:00"},
          {"title": "Men's A,","Division": "M1","Opposition": "Thorpeness","HomeAway":"Home","Location": "Ipswich School Sports Centre, The Street, Rushmere","start": "2024-03-13T20:00:00"},
          {"title": "Men's B,","Division": "M2","Opposition": "Felixstowe","HomeAway":"Home","Location": "Ipswich School Sports Centre, The Street, Rushmere","start": "2024-03-13T20:00:00"},
          {"title": "Mixed A,","Division": "Mx1","Opposition": "Felixstowe","HomeAway":"Home","Location": "Ipswich School Sports Centre, The Street, Rushmere","start": "2024-03-18T20:00:00"},
          {"title": "Ladies B,","Division": "L1","Opposition": "Stowmarket","HomeAway":"Home","Location": "Ipswich School Sports Centre, The Street, Rushmere","start": "2024-03-20T20:00:00"},
          {"title": "Men's D,","Division": "M4","Opposition": "Stowmarket","HomeAway":"Home","Location": "Ipswich School Sports Centre, The Street, Rushmere","start": "2024-03-20T20:00:00"},
          {"title": "Ladies A,","Division": "L1","Opposition": "Stowmarket","HomeAway":"Away","Location": "Mid Suffolk Leisure Centre","start": "2024-03-25T20:00:00"},
          {"title": "Men's A,","Division": "M1","Opposition": "Stowmarket","HomeAway":"Away","Location": "Mid Suffolk Leisure Centre","start": "2024-03-25T20:00:00"},
          {"title": "Men's B,","Division": "M2","Opposition": "Glevering","HomeAway":"Home","Location": "Ipswich School Sports Centre, The Street, Rushmere","start": "2024-03-27T20:00:00"},
          {"title": "Ladies A","Division": "L1","Opposition": "Belstead & Bergholt","HomeAway": "Home","start": "2024-10-02T20:00:00","Location": "Ipswich School Sports Centre, Rushmere" },
          {"title": "Open A","Division": "O1","Opposition": "Belstead & Bergholt","HomeAway": "Home","start": "2024-10-02T20:00:00","Location": "Ipswich School Sports Centre, Rushmere" },
          {"title": "Open B","Division": "O2","Opposition": "Ipswich Tigers","HomeAway": "Away","start": "2024-10-07T20:00:00","Location": "Inspire Suffolk, Lindbergh Road, Ipswich, IP3 9QX" },
          {"title": "Open A","Division": "O1","Opposition": "Ipswich YM Exiles","HomeAway": "Away","start": "2024-10-09T19:00:00","Location": "(Suffolk) One, Scrivener Drive, Ipswich, IP8 0SU" },
          {"title": "Open C","Division": "O4","Opposition": "Skillcentre","HomeAway": "Away","start": "2024-10-10T19:15:00","Location": "Handford Hall School, Ipswich, IP1 2LQ" },
          {"title": "Ladies A","Division": "L1","Opposition": "Felixstowe","HomeAway": "Away","start": "2024-10-14T19:00:00","Location": "Brackenbury Sports Centre, High Road East, Felixstowe" },
          {"title": "Mixed C","Division": "Mx5","Opposition": "Thorpeness","HomeAway": "Home","start": "2024-10-14T20:00:00","Location": "Ipswich School Sports Centre, Rushmere" },
          {"title": "Open B","Division": "O2","Opposition": "DVE","HomeAway": "Home","start": "2024-10-16T20:00:00","Location": "Ipswich School Sports Centre, Rushmere" },
          {"title": "Mixed A","Division": "Mx1","Opposition": "Ipswich YM Exiles","HomeAway": "Away","start": "2024-10-16T19:00:00","Location": "(Suffolk) One, Scrivener Drive, Ipswich, IP8 0SU" },
          {"title": "Mixed B","Division": "Mx2","Opposition": "Leiston","HomeAway": "Away","start": "2024-10-17T20:00:00","Location": "Leiston Sports Centre Red House Lane, Leiston, IP16 4LS" },
          {"title": "Open B","Division": "O2","Opposition": "Felixstowe","HomeAway": "Away","start": "2024-10-21T19:00:00","Location": "Brackenbury Sports Centre, High Road East, Felixstowe" },
          {"title": "Open C","Division": "O4","Opposition": "Corinthians","HomeAway": "Away","start": "2024-10-22T20:30:00","Location": "Ipswich School Sports Hall, 25 Henley Road, Ipswich, IP1 3SG" },
          {"title": "Mixed A","Division": "Mx1","Opposition": "Belstead & Bergholt","HomeAway": "Home","start": "2024-10-23T20:00:00","Location": "Ipswich School Sports Centre, Rushmere" },
          {"title": "Mixed C","Division": "Mx5","Opposition": "Belstead & Bergholt","HomeAway": "Home","start": "2024-10-23T20:00:00","Location": "Ipswich School Sports Centre, Rushmere" },
          {"title": "Ladies B","Division": "L2","Opposition": "Skillcentre","HomeAway": "Away","start": "2024-10-24T19:15:00","Location": "Handford Hall School, Ipswich, IP1 2LQ" },
          {"title": "Open B","Division": "O2","Opposition": "Glevering","HomeAway": "Away","start": "2024-10-29T19:30:00","Location": "Framlingham (College) Junior School, Brandeston, Woodbridge IP13 7AH" },
          {"title": "Mixed A","Division": "Mx1","Opposition": "Stowmarket","HomeAway": "Home","start": "2024-10-30T20:00:00","Location": "Ipswich School Sports Centre, Rushmere" },
          {"title": "Mixed C","Division": "Mx5","Opposition": "Stowmarket","HomeAway": "Home","start": "2024-10-30T20:00:00","Location": "Ipswich School Sports Centre, Rushmere" },
          {"title": "Mixed B","Division": "Mx2","Opposition": "Ipswich YM Exiles","HomeAway": "Home","start": "2024-11-04T20:00:00","Location": "Ipswich School Sports Centre, Rushmere" },
          {"title": "Open A","Division": "O1","Opposition": "Abbeygate","HomeAway": "Away","start": "2024-11-06T19:00:00","Location": "The Dome Sports Hall, King Edward VI School, Bury St Edmunds IP33 3BH" },
          {"title": "Open B","Division": "O2","Opposition": "Abbeygate","HomeAway": "Away","start": "2024-11-06T19:00:00","Location": "The Dome Sports Hall, King Edward VI School, Bury St Edmunds IP33 3BH" },
          {"title": "Mixed C","Division": "Mx5","Opposition": "Woodbridge","HomeAway": "Away","start": "2024-11-07T19:30:00","Location": "Kesgrave High School, Main Road, Kesgrave, IP5 2PB" },
          {"title": "Ladies A","Division": "L1","Opposition": "Corinthians","HomeAway": "Away","start": "2024-11-12T20:30:00","Location": "Ipswich School Sports Hall, 25 Henley Road, Ipswich, IP1 3SG" },
          {"title": "Open A","Division": "O1","Opposition": "Corinthians","HomeAway": "Away","start": "2024-11-12T20:30:00","Location": "Ipswich School Sports Hall, 25 Henley Road, Ipswich, IP1 3SG" },
          {"title": "Open B","Division": "O2","Opposition": "Abbeygate","HomeAway": "Home","start": "2024-11-13T20:00:00","Location": "Ipswich School Sports Centre, Rushmere" },
          {"title": "Ladies B","Division": "L2","Opposition": "Ipswich YM Exiles","HomeAway": "Away","start": "2024-11-13T19:00:00","Location": "(Suffolk) One, Scrivener Drive, Ipswich, IP8 0SU" },
          {"title": "Open C","Division": "O4","Opposition": "Leiston","HomeAway": "Home","start": "2024-11-13T20:00:00","Location": "Ipswich School Sports Centre, Rushmere" },
          {"title": "Ladies A","Division": "L1","Opposition": "Stowmarket","HomeAway": "Away","start": "2024-11-18T20:00:00","Location": "Mid Suffolk Leisure Centre, Gainsborough Road, Stowmarket, IP14 1LH" },
          {"title": "Open A","Division": "O1","Opposition": "Stowmarket","HomeAway": "Away","start": "2024-11-18T20:00:00","Location": "Mid Suffolk Leisure Centre, Gainsborough Road, Stowmarket, IP14 1LH" },
          {"title": "Mixed A","Division": "Mx1","Opposition": "Corinthians","HomeAway": "Home","start": "2024-11-20T20:00:00","Location": "Ipswich School Sports Centre, Rushmere" },
          {"title": "Mixed B","Division": "Mx2","Opposition": "DVE","HomeAway": "Home","start": "2024-11-20T20:00:00","Location": "Ipswich School Sports Centre, Rushmere" },
          {"title": "Open C","Division": "O4","Opposition": "Ipswich Tigers","HomeAway": "Away","start": "2024-11-25T20:00:00","Location": "Inspire Suffolk, Lindbergh Road, Ipswich, IP3 9QX" },
          {"title": "Ladies B","Division": "L2","Opposition": "DVE","HomeAway": "Home","start": "2024-11-27T20:00:00","Location": "Ipswich School Sports Centre, Rushmere" },
          {"title": "Mixed B","Division": "Mx2","Opposition": "Thorpeness","HomeAway": "Away","start": "2024-11-29T19:00:00","Location": "Wickham Market Primary School, Dallinghoo Road, IP13 0RP" },
          {"title": "Mixed A","Division": "Mx1","Opposition": "Ipswich YM Exiles","HomeAway": "Home","start": "2024-12-02T20:00:00","Location": "Ipswich School Sports Centre, Rushmere" },
          {"title": "Mixed B","Division": "Mx2","Opposition": "Stowmarket","HomeAway": "Home","start": "2024-12-04T20:00:00","Location": "Ipswich School Sports Centre, Rushmere" },
          {"title": "Ladies A","Division": "L1","Opposition": "Abbeygate","HomeAway": "Away","start": "2024-12-11T19:00:00","Location": "The Dome Sports Hall, King Edward VI School, Bury St Edmunds IP33 3BH" },
          {"title": "Ladies B","Division": "L2","Opposition": "Constitutional ","HomeAway": "Home","start": "2024-12-11T20:00:00","Location": "Ipswich School Sports Centre, Rushmere" },
          {"title": "Open C","Division": "O4","Opposition": "Ipswich YM Exiles","HomeAway": "Home","start": "2024-12-11T20:00:00","Location": "Ipswich School Sports Centre, Rushmere" },
          {"title": "Mixed A","Division": "Mx1","Opposition": "Belstead & Bergholt","HomeAway": "Away","start": "2024-12-16T19:00:00","Location": "(Suffolk) One, Scrivener Drive, Ipswich, IP8 0SU" },
          {"title": "Mixed B","Division": "Mx2","Opposition": "Felixstowe","HomeAway": "Away","start": "2024-12-18T19:00:00","Location": "Brackenbury Sports Centre, High Road East, Felixstowe" },
          {"title": "Ladies B","Division": "L2","Opposition": "Skillcentre","HomeAway": "Home","start": "2024-12-18T20:00:00","Location": "Ipswich School Sports Centre, Rushmere" },
          {"title": "Open C","Division": "O4","Opposition": "Skillcentre","HomeAway": "Home","start": "2024-12-18T20:00:00","Location": "Ipswich School Sports Centre, Rushmere" },
          {"title": "Open B","Division": "O2","Opposition": "DVE","HomeAway": "Away","start": "2025-01-03T19:45:00","Location": "Debenham Sports Centre, Gracechurch Street, Debenham, IP14 6BL" },
          {"title": "Open A","Division": "O1","Opposition": "Thorpeness","HomeAway": "Away","start": "2025-01-03T19:00:00","Location": "Wickham Market Primary School, Dallinghoo Road, IP13 0RP" },
          {"title": "Ladies A","Division": "L1","Opposition": "Corinthians","HomeAway": "Home","start": "2025-01-08T20:00:00","Location": "Ipswich School Sports Centre, Rushmere" },
          {"title": "Open A","Division": "O1","Opposition": "Corinthians","HomeAway": "Home","start": "2025-01-08T20:00:00","Location": "Ipswich School Sports Centre, Rushmere" },
          {"title": "Open C","Division": "O4","Opposition": "Leiston","HomeAway": "Away","start": "2025-01-09T20:00:00","Location": "Leiston Sports Centre Red House Lane, Leiston, IP16 4LS" },
          {"title": "Mixed B","Division": "Mx2","Opposition": "DVE","HomeAway": "Away","start": "2025-01-10T19:45:00","Location": "Debenham Sports Centre, Gracechurch Street, Debenham, IP14 6BL" },
          {"title": "Open A","Division": "O1","Opposition": "Ipswich YM Exiles","HomeAway": "Home","start": "2025-01-13T20:00:00","Location": "Ipswich School Sports Centre, Rushmere" },
          {"title": "Open B","Division": "O2","Opposition": "Needham","HomeAway": "Away","start": "2025-01-14T19:00:00","Location": "Gainsborough Sports Centre" },
          {"title": "Open C","Division": "O4","Opposition": "Corinthians","HomeAway": "Home","start": "2025-01-15T20:00:00","Location": "Ipswich School Sports Centre, Rushmere" },
          {"title": "Mixed B","Division": "Mx2","Opposition": "Felixstowe","HomeAway": "Home","start": "2025-01-15T20:00:00","Location": "Ipswich School Sports Centre, Rushmere" },
          {"title": "Ladies B","Division": "L2","Opposition": "DVE","HomeAway": "Away","start": "2025-01-17T19:45:00","Location": "Debenham Sports Centre, Gracechurch Street, Debenham, IP14 6BL" },
          {"title": "Ladies A","Division": "L1","Opposition": "Felixstowe","HomeAway": "Home","start": "2025-01-22T20:00:00","Location": "Ipswich School Sports Centre, Rushmere" },
          {"title": "Open B","Division": "O2","Opposition": "Felixstowe","HomeAway": "Home","start": "2025-01-22T20:00:00","Location": "Ipswich School Sports Centre, Rushmere" },
          {"title": "Open C","Division": "O4","Opposition": "Woodbridge","HomeAway": "Away","start": "2025-01-23T19:30:00","Location": "Kesgrave High School, Main Road, Kesgrave, IP5 2PB" },
          {"title": "Open D","Division": "O5","Opposition": "Felixstowe","HomeAway": "Away","start": "2025-01-27T19:30:00","Location": "Brackenbury Sports Centre, High Road East, Felixstowe" },
          {"title": "Mixed C","Division": "Mx5","Opposition": "Woodbridge","HomeAway": "Home","start": "2025-01-27T20:00:00","Location": "Ipswich School Sports Centre, Rushmere" },
          {"title": "Open A","Division": "O1","Opposition": "Thorpeness","HomeAway": "Home","start": "2025-01-29T20:00:00","Location": "Ipswich School Sports Centre, Rushmere" },
          {"title": "Mixed A","Division": "Mx1","Opposition": "Stowmarket","HomeAway": "Away","start": "2025-02-03T20:00:00","Location": "Mid Suffolk Leisure Centre, Gainsborough Road, Stowmarket, IP14 1LH" },
          {"title": "Mixed C","Division": "Mx5","Opposition": "Stowmarket","HomeAway": "Away","start": "2025-02-03T20:00:00","Location": "Mid Suffolk Leisure Centre, Gainsborough Road, Stowmarket, IP14 1LH" },
          {"title": "Open B","Division": "O2","Opposition": "Glevering","HomeAway": "Home","start": "2025-02-05T20:00:00","Location": "Ipswich School Sports Centre, Rushmere" },
          {"title": "Mixed B","Division": "Mx2","Opposition": "Ipswich YM Exiles","HomeAway": "Away","start": "2025-02-05T19:00:00","Location": "(Suffolk) One, Scrivener Drive, Ipswich, IP8 0SU" },
          {"title": "Mixed A","Division": "Mx1","Opposition": "Belstead & Bergholt","HomeAway": "Away","start": "2025-02-10T19:00:00","Location": "(Suffolk) One, Scrivener Drive, Ipswich, IP8 0SU" },
          {"title": "Mixed C","Division": "Mx5","Opposition": "Belstead & Bergholt","HomeAway": "Away","start": "2025-02-10T19:00:00","Location": "(Suffolk) One, Scrivener Drive, Ipswich, IP8 0SU" },
          {"title": "Mixed A","Division": "Mx1","Opposition": "Abbeygate","HomeAway": "Away","start": "2025-02-12T19:00:00","Location": "The Dome Sports Hall, King Edward VI School, Bury St Edmunds IP33 3BH" },
          {"title": "Ladies B","Division": "L2","Opposition": "Ipswich YM Exiles","HomeAway": "Home","start": "2025-02-12T20:00:00","Location": "Ipswich School Sports Centre, Rushmere" },
          {"title": "Mixed B","Division": "Mx2","Opposition": "Thorpeness","HomeAway": "Home","start": "2025-02-17T20:00:00","Location": "Ipswich School Sports Centre, Rushmere" },
          {"title": "Ladies A","Division": "L1","Opposition": "Abbeygate","HomeAway": "Home","start": "2025-02-19T20:00:00","Location": "Ipswich School Sports Centre, Rushmere" },
          {"title": "Open A","Division": "O1","Opposition": "Abbeygate","HomeAway": "Home","start": "2025-02-19T20:00:00","Location": "Ipswich School Sports Centre, Rushmere" },
          {"title": "Open C","Division": "O4","Opposition": "Ipswich YM Exiles","HomeAway": "Away","start": "2025-02-19T19:00:00","Location": "(Suffolk) One, Scrivener Drive, Ipswich, IP8 0SU" },
          {"title": "Mixed C","Division": "Mx5","Opposition": "Thorpeness","HomeAway": "Away","start": "2025-02-21T19:00:00","Location": "Wickham Market Primary School, Dallinghoo Road, IP13 0RP" },
          {"title": "Ladies A","Division": "L1","Opposition": "Belstead & Bergholt","HomeAway": "Away","start": "2025-02-24T19:00:00","Location": "(Suffolk) One, Scrivener Drive, Ipswich, IP8 0SU" },
          {"title": "Open A","Division": "O1","Opposition": "Belstead & Bergholt","HomeAway": "Away","start": "2025-02-24T19:00:00","Location": "(Suffolk) One, Scrivener Drive, Ipswich, IP8 0SU" },
          {"title": "Open B","Division": "O2","Opposition": "Ipswich Tigers","HomeAway": "Home","start": "2025-02-26T20:00:00","Location": "Ipswich School Sports Centre, Rushmere" },
          {"title": "Open C","Division": "O4","Opposition": "Ipswich Tigers","HomeAway": "Home","start": "2025-02-26T20:00:00","Location": "Ipswich School Sports Centre, Rushmere" },
          {"title": "Mixed A","Division": "Mx1","Opposition": "Abbeygate","HomeAway": "Home","start": "2025-03-05T20:00:00","Location": "Ipswich School Sports Centre, Rushmere" },
          {"title": "Mixed B","Division": "Mx2","Opposition": "Leiston","HomeAway": "Home","start": "2025-03-05T20:00:00","Location": "Ipswich School Sports Centre, Rushmere" },
          {"title": "Mixed A","Division": "Mx1","Opposition": "Corinthians","HomeAway": "Away","start": "2025-03-11T20:30:00","Location": "Ipswich School Sports Hall, 25 Henley Road, Ipswich, IP1 3SG" },
          {"title": "Open B","Division": "O2","Opposition": "Needham","HomeAway": "Home","start": "2025-03-12T20:00:00","Location": "Ipswich School Sports Centre, Rushmere" },
          {"title": "Mixed B","Division": "Mx2","Opposition": "Stowmarket","HomeAway": "Away","start": "2025-03-17T20:00:00","Location": "Mid Suffolk Leisure Centre, Gainsborough Road, Stowmarket, IP14 1LH" },
          {"title": "Ladies B","Division": "L2","Opposition": "Constitutional ","HomeAway": "Away","start": "2025-03-18T19:00:00","Location": "Skyliner Sports Centre, Rougham Tower Ave, Bury St. Edmunds IP32 7QB" },
          {"title": "Open C","Division": "O4","Opposition": "Woodbridge","HomeAway": "Home","start": "2025-03-19T20:00:00","Location": "Ipswich School Sports Centre, Rushmere" },
          {"title": "Ladies A","Division": "L1","Opposition": "Stowmarket","HomeAway": "Home","start": "2025-03-26T20:00:00","Location": "Ipswich School Sports Centre, Rushmere" },
          {"title": "Open A","Division": "O1","Opposition": "Stowmarket","HomeAway": "Home","start": "2025-03-26T20:00:00","Location": "Ipswich School Sports Centre, Rushmere" },
          {"title": "Mixed A","Division": "Mx1","Opposition": "Belstead & Bergholt","HomeAway": "Home","start": "2025-03-31T20:00:00","Location": "Ipswich School Sports Centre, Rushmere" },
          {"title": "Playford Trophy","Division": "Mx1","Opposition": "Ipswich YM Exiles","HomeAway": "Away","start": "2024-12-04T19:00:00","Location": "Suffolk One, Scrivener Drive, Ipswich" },
          {
            "title": "Mixed C",
            "Division": "Mx4",
            "Opposition": "BSP Drakes",
            "HomeAway": "Away",
            "Location": "Ipswich School, Henley Road",
            "start": "2025-09-17T20:00:00"
          },
          {
            "title": "Open A",
            "Division": "O1",
            "Opposition": "Corinthians",
            "HomeAway": "Away",
            "Location": "Ipswich School, Henley Road",
            "start": "2025-09-30T20:30:00"
          },
          {
            "title": "Open B",
            "Division": "O2",
            "Opposition": "Felixstowe",
            "HomeAway": "Away",
            "Location": "Brackenberry Sports Centre",
            "start": "2025-01-10T19:00:00"
          },
          {
            "title": "Open C",
            "Division": "O4",
            "Opposition": "Skillcentre",
            "HomeAway": "Away",
            "Location": "Chantry High School",
            "start": "2025-02-10T19:00:00"
          },
          {
            "title": "Mixed A",
            "Division": "Mx1",
            "Opposition": "Belstead & Bergholt",
            "HomeAway": "Away",
            "Location": "Suffolk One",
            "start": "2025-06-10T19:00:00"
          },
          {
            "title": "Open C",
            "Division": "O4",
            "Opposition": "Stradbroke",
            "HomeAway": "Away",
            "Location": "Hartismere High School Castleton Way Eye Suffolk  IP23 7BL",
            "start": "2025-07-10T19:00:00"
          },
          {
            "title": "Open B",
            "Division": "O2",
            "Opposition": "Stowmarket",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, Rushmere",
            "start": "2025-08-10T20:00:00"
          },
          {
            "title": "Ladies A",
            "Division": "L1",
            "Opposition": "Stowmarket",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, Rushmere",
            "start": "2025-08-10T20:00:00"
          },
          {
            "title": "Open B",
            "Division": "O2",
            "Opposition": "Stowmarket",
            "HomeAway": "Away",
            "Location": "Mid Suffolk Leisure Centre",
            "start": "2025-10-13T20:00:00"
          },
          {
            "title": "Open C",
            "Division": "O4",
            "Opposition": "Corinthians",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, Rushmere",
            "start": "2025-10-15T20:00:00"
          },
          {
            "title": "Ladies A",
            "Division": "L1",
            "Opposition": "Corinthians",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, Rushmere",
            "start": "2025-10-15T20:00:00"
          },
          {
            "title": "Mixed A",
            "Division": "Mx1",
            "Opposition": "Stowmarket",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, Rushmere",
            "start": "2025-10-20T20:00:00"
          },
          {
            "title": "Open B",
            "Division": "O2",
            "Opposition": "Corinthians",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, Rushmere",
            "start": "2025-10-22T20:00:00"
          },
          {
            "title": "Open C",
            "Division": "O4",
            "Opposition": "Skillcentre",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, Rushmere",
            "start": "2025-10-22T20:00:00"
          },
          {
            "title": "Mixed B",
            "Division": "Mx2",
            "Opposition": "Leiston",
            "HomeAway": "Away",
            "Location": "Leiston Sports Centre, Red House Lane, Leiston, IP16 4LS",
            "start": "2025-10-23T20:00:00"
          },
          {
            "title": "Mixed B",
            "Division": "Mx2",
            "Opposition": "Stowmarket",
            "HomeAway": "Away",
            "Location": "Mid Suffolk Leisure Centre",
            "start": "2025-10-29T20:00:00"
          },
          {
            "title": "Open B",
            "Division": "O2",
            "Opposition": "DVE",
            "HomeAway": "Away",
            "Location": "Debenham Sports and Leisure Centre",
            "start": "2026-01-23T19:45:00"
          },
          {
            "title": "Open C",
            "Division": "O4",
            "Opposition": "DVE",
            "HomeAway": "Away",
            "Location": "Debenham Sports and Leisure Centre",
            "start": "2025-10-31T19:45:00"
          },
          {
            "title": "Mixed C",
            "Division": "Mx4",
            "Opposition": "BSP Drakes",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, Rushmere",
            "start": "2025-03-11T20:00:00"
          },
          {
            "title": "Open B",
            "Division": "O2",
            "Opposition": "Framlingham & Glevering",
            "HomeAway": "Away",
            "Location": "Framlingham College Prep School, Brandeston. IP13 7AH",
            "start": "2025-04-11T19:30:00"
          },
          {
            "title": "Open A",
            "Division": "O1",
            "Opposition": "Abbeygate",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, Rushmere",
            "start": "2025-05-11T20:00:00"
          },
          {
            "title": "Ladies A",
            "Division": "L1",
            "Opposition": "Abbeygate",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, Rushmere",
            "start": "2025-05-11T20:00:00"
          },
          {
            "title": "Mixed A",
            "Division": "Mx1",
            "Opposition": "Corinthians",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, Rushmere",
            "start": "2025-10-11T20:00:00"
          },
          {
            "title": "Mixed B",
            "Division": "Mx2",
            "Opposition": "Skillcentre",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, Rushmere",
            "start": "2025-12-11T20:00:00"
          },
          {
            "title": "Mixed C",
            "Division": "Mx4",
            "Opposition": "Skillcentre",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, Rushmere",
            "start": "2025-12-11T20:00:00"
          },
          {
            "title": "Open A",
            "Division": "O1",
            "Opposition": "Ipswich Tigers",
            "HomeAway": "Away",
            "Location": "Inspire Suffolk",
            "start": "2025-11-17T20:00:00"
          },
          {
            "title": "Open C",
            "Division": "O4",
            "Opposition": "Woodbridge",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, Rushmere",
            "start": "2025-11-17T20:00:00"
          },
          {
            "title": "Open A",
            "Division": "O1",
            "Opposition": "Belstead & Bergholt",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, Rushmere",
            "start": "2025-11-19T20:00:00"
          },
          {
            "title": "Ladies A",
            "Division": "L1",
            "Opposition": "Belstead & Bergholt",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, Rushmere",
            "start": "2025-11-19T20:00:00"
          },
          {
            "title": "Mixed B",
            "Division": "Mx2",
            "Opposition": "Corinthians",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, Rushmere",
            "start": "2025-11-24T20:00:00"
          },
          {
            "title": "Mixed A",
            "Division": "Mx1",
            "Opposition": "Ipswich YM Exiles",
            "HomeAway": "Away",
            "Location": "Suffolk One",
            "start": "2025-11-26T19:00:00"
          },
          {
            "title": "Open A",
            "Division": "O1",
            "Opposition": "Thorpeness",
            "HomeAway": "Away",
            "Location": "Wickham Market Primary Schoo",
            "start": "2026-02-17T19:00:00"
          },
          {
            "title": "Open A",
            "Division": "O1",
            "Opposition": "Ipswich YM Exiles",
            "HomeAway": "Away",
            "Location": "Suffolk One",
            "start": "2025-03-12T19:00:00"
          },
          {
            "title": "Ladies A",
            "Division": "L1",
            "Opposition": "Ipswich YM Exiles",
            "HomeAway": "Away",
            "Location": "Suffolk One",
            "start": "2025-03-12T19:00:00"
          },
          {
            "title": "Mixed C",
            "Division": "Mx4",
            "Opposition": "Constitutional ",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, Rushmere",
            "start": "2025-08-12T20:00:00"
          },
          {
            "title": "Mixed A",
            "Division": "Mx1",
            "Opposition": "Abbeygate",
            "HomeAway": "Away",
            "Location": "King Edward VI School, Bury St Edmunds IP33 3BH",
            "start": "2025-10-12T19:00:00"
          },
          {
            "title": "Mixed B",
            "Division": "Mx2",
            "Opposition": "Ipswich YM Exiles",
            "HomeAway": "Away",
            "Location": "Suffolk One",
            "start": "2025-10-12T19:00:00"
          },
          {
            "title": "Mixed B",
            "Division": "Mx2",
            "Opposition": "Thorpeness",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, Rushmere",
            "start": "2025-12-15T20:00:00"
          },
          {
            "title": "Mixed A",
            "Division": "Mx1",
            "Opposition": "Belstead & Bergholt",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, Rushmere",
            "start": "2025-12-17T20:00:00"
          },
          {
            "title": "Mixed C",
            "Division": "Mx4",
            "Opposition": "Felixstowe",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, Rushmere",
            "start": "2025-12-17T20:00:00"
          },
          {
            "title": "Open B",
            "Division": "O2",
            "Opposition": "Stowmarket",
            "HomeAway": "Away",
            "Location": "Mid Suffolk Leisure Centre",
            "start": "2026-01-05T20:00:00"
          },
          {
            "title": "Ladies A",
            "Division": "L1",
            "Opposition": "Stowmarket",
            "HomeAway": "Away",
            "Location": "Mid Suffolk Leisure Centre",
            "start": "2026-01-05T20:00:00"
          },
          {
            "title": "Open A",
            "Division": "O1",
            "Opposition": "Thorpeness",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, Rushmere",
            "start": "2026-01-05T20:00:00"
          },
          {
            "title": "Open C",
            "Division": "O4",
            "Opposition": "Skillcentre",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, Rushmere",
            "start": "2026-01-07T20:00:00"
          },
          {
            "title": "Mixed B",
            "Division": "Mx2",
            "Opposition": "Leiston",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, Rushmere",
            "start": "2026-01-07T20:00:00"
          },
          {
            "title": "Open B",
            "Division": "O2",
            "Opposition": "Stowmarket",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, Rushmere",
            "start": "2026-01-12T20:00:00"
          },
          {
            "title": "Open A",
            "Division": "O1",
            "Opposition": "Abbeygate",
            "HomeAway": "Away",
            "Location": "King Edward VI School, Bury St Edmunds IP33 3BH",
            "start": "2026-01-14T19:00:00"
          },
          {
            "title": "Ladies A",
            "Division": "L1",
            "Opposition": "Abbeygate",
            "HomeAway": "Away",
            "Location": "King Edward VI School, Bury St Edmunds IP33 3BH",
            "start": "2026-01-14T19:00:00"
          },
          {
            "title": "Mixed B",
            "Division": "Mx2",
            "Opposition": "Ipswich YM Exiles",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, Rushmere",
            "start": "2026-01-19T20:00:00"
          },
          {
            "title": "Mixed C",
            "Division": "Mx4",
            "Opposition": "Constitutional ",
            "HomeAway": "Away",
            "Location": "Skyliner Sports Centre, Rougham Tower Ave, Bury St.Edmunds IP32 7QB",
            "start": "2026-01-20T19:00:00"
          },
          {
            "title": "Mixed A",
            "Division": "Mx1",
            "Opposition": "Stowmarket",
            "HomeAway": "Away",
            "Location": "Mid Suffolk Leisure Centre",
            "start": "2026-01-21T20:00:00"
          },
          {
            "title": "Open C",
            "Division": "O4",
            "Opposition": "Woodbridge",
            "HomeAway": "Away",
            "Location": "Kesgrave High School",
            "start": "2026-01-22T19:30:00"
          },
          {
            "title": "Mixed A",
            "Division": "Mx1",
            "Opposition": "Corinthians",
            "HomeAway": "Away",
            "Location": "Ipswich School, Henley Road",
            "start": "2026-01-27T20:30:00"
          },
          {
            "title": "Open C",
            "Division": "O4",
            "Opposition": "Skillcentre",
            "HomeAway": "Away",
            "Location": "Chantry High School",
            "start": "2026-01-29T19:00:00"
          },
          {
            "title": "Mixed A",
            "Division": "Mx1",
            "Opposition": "Abbeygate",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, Rushmere",
            "start": "2026-02-02T20:00:00"
          },
          {
            "title": "Open B",
            "Division": "O2",
            "Opposition": "Corinthians",
            "HomeAway": "Away",
            "Location": "Ipswich School, Henley Road",
            "start": "2026-02-03T20:30:00"
          },
          {
            "title": "Open C",
            "Division": "O4",
            "Opposition": "Corinthians",
            "HomeAway": "Away",
            "Location": "Ipswich School, Henley Road",
            "start": "2026-02-03T20:30:00"
          },
          {
            "title": "Mixed B",
            "Division": "Mx2",
            "Opposition": "Thorpeness",
            "HomeAway": "Away",
            "Location": "Wickham Market Primary Schoo",
            "start": "2026-02-06T19:00:00"
          },
          {
            "title": "Open A",
            "Division": "O1",
            "Opposition": "Ipswich Tigers",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, Rushmere",
            "start": "2026-02-09T20:00:00"
          },
          {
            "title": "Mixed A",
            "Division": "Mx1",
            "Opposition": "Ipswich YM Exiles",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, Rushmere",
            "start": "2026-02-11T20:00:00"
          },
          {
            "title": "Mixed B",
            "Division": "Mx2",
            "Opposition": "Stowmarket",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, Rushmere",
            "start": "2026-02-11T20:00:00"
          },
          {
            "title": "Open B",
            "Division": "O2",
            "Opposition": "Framlingham & Glevering",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, Rushmere",
            "start": "2026-02-16T20:00:00"
          },
          {
            "title": "Mixed B",
            "Division": "Mx2",
            "Opposition": "Skillcentre",
            "HomeAway": "Away",
            "Location": "Chantry High School",
            "start": "2026-02-19T19:00:00"
          },
          {
            "title": "Mixed C",
            "Division": "Mx4",
            "Opposition": "Skillcentre",
            "HomeAway": "Away",
            "Location": "Chantry High School",
            "start": "2026-02-19T19:00:00"
          },
          {
            "title": "Open A",
            "Division": "O1",
            "Opposition": "Corinthians",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, Rushmere",
            "start": "2026-02-23T20:00:00"
          },
          {
            "title": "Ladies A",
            "Division": "L1",
            "Opposition": "Corinthians",
            "HomeAway": "Away",
            "Location": "Ipswich School, Henley Road",
            "start": "2026-02-24T20:30:00"
          },
          {
            "title": "Open B",
            "Division": "O2",
            "Opposition": "Felixstowe",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, Rushmere",
            "start": "2026-02-25T20:00:00"
          },
          {
            "title": "Open C",
            "Division": "O4",
            "Opposition": "Stradbroke",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, Rushmere",
            "start": "2026-02-25T20:00:00"
          },
          {
            "title": "Open A",
            "Division": "O1",
            "Opposition": "Ipswich YM Exiles",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, Rushmere",
            "start": "2026-03-04T20:00:00"
          },
          {
            "title": "Ladies A",
            "Division": "L1",
            "Opposition": "Ipswich YM Exiles",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, Rushmere",
            "start": "2026-04-03T20:00:00"
          },
          {
            "title": "Mixed B",
            "Division": "Mx2",
            "Opposition": "Corinthians",
            "HomeAway": "Away",
            "Location": "Ipswich School, Henley Road",
            "start": "2026-03-10T20:30:00"
          },
          {
            "title": "Mixed A",
            "Division": "Mx1",
            "Opposition": "Belstead & Bergholt",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, Rushmere",
            "start": "2026-03-11T20:00:00"
          },
          {
            "title": "Mixed C",
            "Division": "Mx4",
            "Opposition": "Belstead & Bergholt",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, Rushmere",
            "start": "2026-03-11T20:00:00"
          },
          {
            "title": "Open A",
            "Division": "O1",
            "Opposition": "Belstead & Bergholt",
            "HomeAway": "Away",
            "Location": "Suffolk One",
            "start": "2026-03-16T19:00:00"
          },
          {
            "title": "Ladies A",
            "Division": "L1",
            "Opposition": "Belstead & Bergholt",
            "HomeAway": "Away",
            "Location": "Suffolk One",
            "start": "2026-03-16T19:00:00"
          },
          {
            "title": "Open B",
            "Division": "O2",
            "Opposition": "DVE",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, Rushmere",
            "start": "2026-03-18T20:00:00"
          },
          {
            "title": "Open C",
            "Division": "O4",
            "Opposition": "DVE",
            "HomeAway": "Home",
            "Location": "Ipswich School Sports Centre, Rushmere",
            "start": "2026-03-18T20:00:00"
          },
          {
            "title": "Mixed C",
            "Division": "Mx4",
            "Opposition": "Felixstowe",
            "HomeAway": "Away",
            "Location": "Brackenberry Sports Centre",
            "start": "2026-03-23T19:00:00"
          },
          {
            "title": "Mixed A",
            "Division": "Mx1",
            "Opposition": "Belstead & Bergholt",
            "HomeAway": "Away",
            "Location": "Suffolk One",
            "start": "2026-03-30T19:00:00"
          },
          {
            "title": "Mixed C",
            "Division": "Mx4",
            "Opposition": "Belstead & Bergholt",
            "HomeAway": "Away",
            "Location": "Suffolk One",
            "start": "2026-03-30T19:00:00"
          },
          {"title": "Playford Trophy","Division": "Mx1","Opposition": "Abbeygate","HomeAway": "Home","start": "2025-10-13T20:00:00","Location": "Ipswich School Sports Centre, Rushmere" },

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
