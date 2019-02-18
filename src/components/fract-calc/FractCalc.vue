<template>
  <div class="fract-calc">
    <div class="fract-calc__box" v-if="data.items && data.items.length">
      <div class="fract-calc__item"  v-for="(item, index) in data.items">
          <fract-calc-fraction
            v-if="item.type == 'fraction'"
            v-bind:item="item"
            v-bind:index="index"
            @removeElement="removeElement">
          </fract-calc-fraction>
          <fract-calc-operation  v-else-if="item.type == 'operation'" v-bind:item="item"></fract-calc-operation>
      </div>
      <div class="fract-calc__item">
          <span class="fract-calc-operation">=</span>
      </div>
      <div class="fract-calc__item">
          <div class="fract-calc__res">{{ result }}</div>
      </div>
    </div>
    <b-button variant="secondary" size="xs" class="fract-calc__btn" v-if="data.items && (data.items.length < 8)" v-on:click="addElement">Добавить дробь</b-button>
  </div>
</template>

<script>
  import FractCalcFraction from '@/components/fract-calc/FractCalcFraction.vue';
  import FractCalcOperation from '@/components/fract-calc/FractCalcOperation.vue';

  export default {
    name: 'FractCalc',
    props: {
      data: Object
    },
    components: {
      FractCalcFraction,
      FractCalcOperation
    },
    methods: {
      calcItem(item) {
        let res = 0;
        if(item && item.numerator && item.denominator) {
          res = item.numerator / item.denominator;
        }
        return res;
      },
      addElement() {
        this.data.items.push({
          type: 'operation',
          value: '+'
        }, {
          type: 'fraction',
          numerator: null,
          denominator: null
        });
      },
      removeElement(index) {
        this.data.items.splice( (index - 1), 2);
      },
    },
    computed: {
      result() {
        const items = this.data.items.filter(el => el.type === 'fraction'),
          self = this;
        let res = 0;
        items.map(function (item) {
            res += self.calcItem(item);
        });
        res = !isNaN( parseFloat(res) ) && isFinite(res) && (res > 0) ? res : null;
        this.data.result = res;
        return res || '?';
      }
    }
  }
</script>

<style lang="scss">
  @import 'fract-calc';
</style>
