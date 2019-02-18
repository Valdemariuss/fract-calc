<template>
  <div class="fract-calc-operation">
    <b-badge class="fract-calc-operation__badge" variant="secondary" size="lg">
      {{ item.value }}
    </b-badge>
  </div>
</template>

<script>
export default {
  name: 'FractCalcOperation',
  props: {
    item: Object
  }
}
</script>
