<template>
  <div>
    <NavBar/>
    <div class="table-container">
      <h1 class="title">GEPLANDE GAMES: </h1>
      <div class="divider"/>
      <div class="table-row" v-for="(lobby, index) in lobbies" :key="index">
        <div class="date-container" v-if="shouldRenderDate(lobby, index)">
          <h2 class="date">{{ lobby.date }}</h2>
          <div class="legend-container">
            <p>Organiseerder</p>
            <p>Starttijd</p>
            <p>Inschrijving</p>
            <p>Stream</p>
          </div>
        </div>
        <div class="row-container">
          <p>{{ lobby.name }}</p>
          <p>{{ lobby.time }}</p>
          <p><a :href="checkUrl(lobby.signUpLink)">{{ lobby.signUpLink }}</a></p>
          <p><a :href="checkUrl(lobby.streamLink)">{{ lobby.streamLink }}</a></p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

import { checkUrl } from '@/utils/functions'
import NavBar from '@/components/NavBar'

export default {
  data() {
    return {
    }
  },
  computed: {
    lobbies() {
      return this.$store.getters.getUpcomingEvents
    }
  },
  components: {
    NavBar
  },
  methods: {
    checkUrl,
    shouldRenderDate(lobby, index) {
      if(this.lobbies[index - 1])
        if(lobby.date !== this.lobbies[index - 1].date) return true
        else return false
      else return true
    }
  }
}
</script>

<style scoped>
.title {
  font-size: 40px;
  font-family: 'Oswald', sans-serif;
  text-align: left;
  color: rgba(59, 59, 59, 1);
}

.table-container {
  margin: 0 auto;
  width: 70%;
}

.table-row {
  width: 100%;
  display: flex;
  flex-direction: column;
}

.date-container {
  width: 100%;
  display: flex;
  flex-direction: column;
}

.date-container h2 {
  color:  rgb(59, 59, 59);
  align-self: flex-start;
}

.date {
  margin-top: 10px !important;
}

.divider {
  width: 100%;
  height: 1px;
  background-color:  rgba(59, 59, 59, 0.5);
  margin-bottom: 10px;
}

.row-container {
  width: 100%;
  display: flex;
  justify-content: space-between;
}

.row-container p {
  width: 25%;
  text-align: left;
  text-overflow: ellipsis;
  overflow: hidden;
  margin: 10px 0;
}

.legend-container {
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 5px;
  background-color:  rgba(59, 59, 59, 1);
}

.legend-container p {
  width: 25%;
  margin: 0;
  text-align: left;
  color: white;
}

@media only screen and (max-width: 700px) {
  .table-container {
    width: 95%;
  }

  .legend-container p {
    text-align: center;
    text-overflow: ellipsis;
    overflow: hidden;
  }
}
</style>