<template>
  <form v-on:submit.prevent="submitForm">
    <h2>Edit the status of a flight</h2>
    <div class="field">
      <label class="label">Flight</label>
      <div class="control">
        <div class="select">
          <select
            v-model="selectedFlightId"
          >
            <option disabled value="">Select a flight</option>
            <option
              v-for="flight in flights"
              v-bind:value="flight.id"
              :key="flight.id"
            >
              {{ flight.departureTime }} - {{ flight.cityName }} / {{ flight.airportCode }} - {{ flight.airline  }}
            </option>
          </select>
        </div>
      </div>
    </div>
    <div
      v-if="selectedFlightId !== ''"
      class="field"
    >
      <label class="label">New Status</label>
      <div class="control">
        <label class="radio">
          <input
            type="radio"
            v-model="newStatus"
            value="Departed"
          />
          Departed
        </label>
        <label class="radio">
          <input
            type="radio"
            v-model="newStatus"
            value="Diverted"
          />
          Diverted
        </label>
        <label class="radio">
          <input
            type="radio"
            v-model="newStatus"
            value="Delayed"
          />
          Delayed
        </label>
        <label class="radio">
          <input
            type="radio"
            v-model="newStatus"
            value="Cancelled"
          />
          Cancelled
        </label>
        <label class="radio">
          <input
            type="radio"
            v-model="newStatus"
            value="Other"
          />
          Other (please specify)
        </label>
      </div>
    </div>
    <div
      v-if="newStatus === 'Other'"
      class="field"
    >
      <label class="label">Enter flight status</label>
      <div class="control">
        <input
          type="text"
          v-model="customStatusText"
          placeholder="Enter flight status"
          class="input"
        />
      </div>
    </div>
    <div class="field">
      <div class="control">
        <button
          v-bind:disabled="!isFormValid"
        >
          Submit
        </button>
      </div>
    </div>
  </form>
</template>

<script>
export default {
  name: 'Form',
  props: {
    flights: {
      type: Array,
      default: []
    }
  },
  data() {
    return {
      selectedFlightId: '',
      newStatus: '',
      customStatusText: ''
    }
  },
  computed: {
    isFormValid: function() {
      return this.selectedFlightId !== '' && 
              this.newStatus !== '' &&
              (this.newStatus !== 'Other' || this.customStatusText !== '')
    },
  },
  methods: {
    submitForm() {
      // use custom text if specified
      if (this.newStatus === 'Other') {
        this.newStatus = this.customStatusText
      }

      // emit event and pass the data up to app component
      const updatedFlight = {
        id: this.selectedFlightId,
        status: this.newStatus
      }
      this.$emit('updateFlightStatus', updatedFlight)

      // clear out data
      this.selectedFlightId = '',
      this.newStatus = '',
      this.customStatusText = ''
    }
  }
}
</script>

<style scoped lang="scss">


</style>