<template>
  <div class="flight-board">
    <div class="header">
      <img
        src="../assets/images/departures-icon.svg"
        class="departures-icon"
        alt="Departures icon"
      >
      <h1>Departures</h1>
    </div>
    <div class="content">
      <div class="column-headings">
        <span>Departure time</span>
        <span>City Name</span>
        <span>Code</span>
        <span>Airline</span>
        <span>Gate</span>
        <span>Status</span>
      </div>
      <div class="flight-data">
        <Flight
          v-for="flight in flights"
          :key="flight.id"
          :departure-time="flight.departureTime"
          :city-name="flight.cityName"
          :airport-code="flight.airportCode"
          :airline="flight.airline"
          :departure-gate="flight.departureGate"
          :status="flight.status"
        />
      </div>
    </div>
  </div>
</template>

<script>
import Flight from './Flight.vue'

export default {
  name: 'FlightBoard',
  components: {
    Flight
  },
  props: {
    flights: {
      type: Array,
      default: []
    }
  }
}
</script>

<style scoped lang="scss">
@import '../assets/styles/mixins.scss';

.flight-board {
  width: 90%;
  margin: 1rem 0;
  background: linear-gradient(90deg, #464646 0%, #000000 100%);
}

.header {
  background: radial-gradient(81.65% 10898.53% at 18.35% 50%, #FFEF97 0%, #DFC42E 100%);
  display: flex;
  align-items: center;
  padding: 1.5rem 0;
}

.departures-icon {
  margin: 0 2rem;
}

.content {
  padding: 1rem;
}

.column-headings {
  @include column-layout;
  background: linear-gradient(90deg, #FFFFFF 0%, #AEBCCA 100%);
  border-radius: 10px;
  padding: 0.75rem 1rem 0.75rem 4rem;
  margin-bottom: 1rem;

  span {
    font-size: 18px;
    font-weight: bold;
    line-height: normal;
  }
}

.flight-data {
  height: 400px;
  overflow: auto;
}
</style>
