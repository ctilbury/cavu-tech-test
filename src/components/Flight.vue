<template>
  <div class="flight">
    <span>
      {{ departureTime }}
    </span>
    <span class="yellow-text">
      {{ cityName }}
    </span>
    <span>
      {{ airportCode }}
    </span>
    <span>
      {{ airline }}
    </span>
    <span class="yellow-text">
      {{ departureGate }}
    </span>
    <span
      class="status-label"
      :class="{
        'orange' : statusOrange,
        'blue' : statusBlue,
        'green' : statusGreen
      }"
    >
      {{ status }}
    </span>
  </div>
</template>

<script>
export default {
  name: 'Flight',
  props: {
    departureTime: {
      type: String,
      default: ''
    },
    cityName: {
      type: String,
      default: ''
    },
    airportCode: {
      type: String,
      default: ''
    },
    airline: {
      type: String,
      default: ''
    },
    departureGate: {
      type: String,
      default: ''
    },
    status: {
      type: String,
      default: ''
    }
  },
  computed: {
    statusOrange: function() {
      return this.status.toLowerCase().includes('final call') || this.status.toLowerCase().includes('flight closing')
    },
    statusBlue: function() {
      return this.status.toLowerCase().includes('go to gate') || this.status.toLowerCase().includes('boarding')
    },
    statusGreen: function() {
      return this.status.toLowerCase().includes('departed')
    }
  }
}
</script>

<style scoped lang="scss">
@import '../assets/styles/mixins.scss';
@import '../assets/styles/variables.scss';

.flight {
  @include column-layout;
  border: 2px solid white;
  border-radius: 10px;
  margin-bottom: 1rem;
  padding: 1.5rem 1rem 1.5rem 4rem;
  font-size: 24px;
  font-weight: bold;

  span {
    color: white;
    
    &.yellow-text {
      color: $yellow;
    }

    &.status-label {
      background-color: white;
      color: $almost-black;
      box-shadow: inset 12px 0px 0px $yellow;
      border-top-right-radius: 20px;
      border-bottom-right-radius: 20px;
      padding: 0.5rem 1rem 0.5rem 2rem;

      &.orange {
        color: $orange;
        box-shadow: inset 12px 0px 0px $orange;
      }

      &.blue {
        box-shadow: inset 12px 0px 0px $blue;
      }

      &.green {
        color: $green;
        box-shadow: inset 12px 0px 0px $green;
      }
    }
  }
}
</style>