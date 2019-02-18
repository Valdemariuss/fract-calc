<template>
  <div class="fract-calc-fraction" v-bind:class="classObject">
    <template v-if="index > 2">
      <b-badge variant="danger" class="fract-calc-fraction__remove" v-on:click="removeElement(index)" v-b-tooltip.hover title="Удалить дробь">X</b-badge>
    </template>
    <b-form-input
      size="sm"
      class="fract-calc-fraction__input"
      type="number"
      min="1"
      max="99"
      v-on:keypress="keyFilter"
      v-model="item.numerator"/>
    <hr class="fract-calc-fraction__line">
    <b-form-input
      size="sm"
      class="fract-calc-fraction__input"
      type="number"
      min="1"
      max="99"
      v-on:keypress="keyFilter"
      v-model="item.denominator"/>
  </div>
</template>

<script>
  export default {
    name: 'FractCalcfract',
    props: {
      item: Object,
      index: Number
    },
    methods:{
      removeElement(index) {
        this.$emit('removeElement', index);
      },
      keyFilter(e){
        const el = e.target,
            code = e.which,
            char = String.fromCharCode(code),
            isNom = !isNaN( parseFloat(char) ) && isFinite(char),
            isLength = !el.value || (el.value.length < 2) ? true : false,
            res = isNom && isLength;
        if(!res) { e.preventDefault(); }
        return res;
      }
    },
    computed: {
      classObject () {
        return {
          '_disable': !(this.item.denominator > 0) || !(this.item.numerator > 0)
        }
      }
    }
  }
</script>
