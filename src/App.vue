<template>
  <div id="app">
    <FlightBoard
      :flights="departures"
    />
  </div>
</template>

<script>
import axios from 'axios';
import { v4 as uuidv4 } from 'uuid';
import FlightBoard from './components/FlightBoard.vue'

export default {
  name: 'App',
  components: {
    FlightBoard
  },
  data() {
    return {
      departures: []
    }
  },
  methods: {
    formatFlightData(allDepartures) {
      const formattedFlightData = allDepartures.map(flight => {
        const formattedFlight = {}

        formattedFlight.id = uuidv4()

        flight.scheduledDepartureDateTime ?
          formattedFlight.departureTime = this.handleDate(flight.scheduledDepartureDateTime) :
          formattedFlight.departureTime = ''

        flight.arrivalAirport && flight.arrivalAirport.cityName ?
          formattedFlight.cityName = flight.arrivalAirport.cityName : 
          formattedFlight.cityName = ''

        flight.arrivalAirport && flight.arrivalAirport.code ?
          formattedFlight.airportCode = flight.arrivalAirport.code : 
          formattedFlight.airportCode = ''

        flight.airline && flight.airline.name ?
          formattedFlight.airline = flight.airline.name :
          formattedFlight.airline = ''

        flight.departureGate && flight.departureGate.number ? 
          formattedFlight.departureGate = flight.departureGate.number : 
          formattedFlight.departureGate = ''

        flight.status ? 
          formattedFlight.status = flight.status :
          formattedFlight.status = ''

        return formattedFlight
      })
      this.departures = formattedFlightData
    },
    handleDate(dateString) {
      const timestamp = Date.parse(dateString)
      if (timestamp) {
        const date = new Date(timestamp)
        // make sure we have a leading 0 if the hours or minutes are one digit
        const hours = `0${date.getHours()}`.slice(-2);
        const minutes = `0${date.getMinutes()}`.slice(-2);
        
        return `${hours}.${minutes}`
      } else {
        return ''
      }
    },
    async getFlightData() {
      try {
        const response = await axios.get('https://6315ae3e5b85ba9b11e4cb85.mockapi.io/departures/Flightdata')
        this.formatFlightData(response.data.allDepartures)
      } catch(error) {
        console.log(`error: ${error}`)
      }
    }
  },
  async mounted() {
    await this.getFlightData()
  }
}
</script>

<style lang="scss">
#app {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
