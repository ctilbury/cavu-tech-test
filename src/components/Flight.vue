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
      <span class="yellow-text gate">Gate</span> {{ departureGate }}
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
@import '../assets/styles/variables.scss';

.flight {
  display: grid;
  grid-template-columns: 30% 30% 40%;
  grid-template-rows: repeat(2, auto);
  grid-auto-flow: column;
  grid-gap: 0.25rem;
  align-items: center;
  border: 2px solid white;
  border-radius: 10px;
  margin-bottom: 1rem;
  padding: 0.5rem 1rem;
  font-size: 0.8rem;
  font-weight: bold;
  line-height: normal;

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
      padding: 0.5rem 1rem 0.5rem 1.5rem;

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

@media screen and (min-width: 600px) {
  .flight {
    grid-template-columns: 16% 18% 12% 22% 10% 22%;
    grid-template-rows: auto;
    grid-auto-flow: row;
    grid-gap: 0;
    font-size: 1rem;
  }

  .gate {
    display: none;
  }
}

@media screen and (min-width: 1024px) {
  .flight {
    grid-template-columns: 18% 18% 12% 22% 10% 20%;
    padding: 0.75rem 1rem 0.75rem 2rem;
    font-size: 1.25rem;

    span.status-label {
      padding-left: 2rem;
    }
  }
}

@media screen and (min-width: 1280px) {
  .flight {
    grid-template-columns: 20% 20% 12% 18% 10% 20%;
    padding: 0.75rem 1rem 0.75rem 4rem;
    font-size: 1.5rem;
  }
}

</style>