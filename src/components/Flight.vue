<template>
  <div class="flight">
    <span>06.55</span>
    <span class="yellow">{{ cityName }}</span>
    <span>{{ airportCode }}</span>
    <span>{{ airline }}</span>
    <span class="yellow">{{ departureGate }}</span>
    <span>{{ status }}</span>
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
  }
}
</script>

<style scoped lang="scss">
@import '../assets/styles/mixins.scss';

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
    
    &.yellow {
      color: #F5D836;
    }
  }
}
</style>
