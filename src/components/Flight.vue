<template>
  <div class="flight">
    <span>06.55</span>
    <span class="yellow">Toronto</span>
    <span>YYZ</span>
    <span>Air Canada</span>
    <span class="yellow">A4</span>
    <span>Flight closing</span>
  </div>
</template>

<script>
export default {
  name: 'Flight'
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
