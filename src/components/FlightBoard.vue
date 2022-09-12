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
      <div
        v-if="flights.length > 0"
        class="flight-data"
      >
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
      <div
        v-else
        class="no-flight-data"
      >
        <div
          v-if="!apiCallFailed"
          class="loading"
        />
        <div
          v-else
          class="error-msg"
        >
          Error: could not get flight data.
        </div>

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
    },
    apiCallFailed: {
      type: Boolean,
      default: false
    }
  }
}
</script>

<style scoped lang="scss">

.flight-board {
  width: 90%;
  margin: 1rem 0;
  background: linear-gradient(90deg, #464646 0%, #000000 100%);
}

.header {
  background: radial-gradient(81.65% 10898.53% at 18.35% 50%, #FFEF97 0%, #DFC42E 100%);
  display: flex;
  align-items: center;
  padding: 1rem 0;
}

.departures-icon {
  margin: 0 2rem;
}

h1 {
  color: black;
  font-style: normal;
  font-weight: 700;
  font-size: 1.4rem;
  margin: 0;
}

.content {
  padding: 1rem;
}

.column-headings {
  display: none;
}

.flight-data {
  height: 400px;
  overflow: auto;
}

.no-flight-data {
  height: 400px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.loading {
  width: 3rem;
  height: 3rem;
  border: 3px solid rgba(255,255,255,0.3);
  border-top-color: #fff;
  border-radius: 50%;
  animation: spinner 0.7s linear infinite;
}

@keyframes spinner {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

.error-msg {
  color: white;
}

@media screen and (min-width: 600px) {
  .header {
    padding: 1.2rem 0;
  }

  h1 {
    font-size: 1.8rem
  }

  .column-headings {
    display: grid;
    grid-template-columns: 16% 18% 12% 22% 10% 22%;
    align-items: center;
    background: linear-gradient(90deg, #FFFFFF 0%, #AEBCCA 100%);
    border-radius: 10px;
    margin-bottom: 1rem;
    padding: 0.5rem 1rem;

    span {
      font-size: 0.8rem;
      font-weight: bold;
      line-height: normal;
    }
  }
}

@media screen and (min-width: 1024px) {
  .header {
    padding: 1.5rem 0;
  }

  h1 {
    font-size: 2.2rem
  }

  .column-headings {
    grid-template-columns: 18% 18% 12% 22% 10% 20%;
    padding: 0.75rem 1rem 0.75rem 2rem;

    span {
      font-size: 1rem;
    }
  }
}

@media screen and (min-width: 1280px) {
  h1 {
    font-size: 2.65rem
  }

  .column-headings {
    grid-template-columns: 20% 20% 12% 18% 10% 20%;
    padding: 0.75rem 1rem 0.75rem 4rem;

    span {
      font-size: 1.25rem;
    }
  }
}

</style>
