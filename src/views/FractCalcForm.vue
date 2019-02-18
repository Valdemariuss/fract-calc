<template>
  <div>
    <h1 class="text-center">Сложение дробей</h1>
    <b-form
      @submit="checkForm"
      action=""
      method="post"
    >
      <template v-if="errors.length">
        <b-alert  variant="danger" size="xs" show v-for="error in errors">{{ error }}</b-alert>
      </template>
      <b-form-group>
        <fract-calc v-bind:data="fractions"></fract-calc>
      </b-form-group>
      <b-button variant="primary" size="lg" type="submit">Отправить</b-button>
      <template v-if="submit">
        <br><br><br>
        <b-alert variant="success" size="xs" show>
          Отправляются данные: <br>
          {{ fractions | json }}
      </b-alert>
      </template>
    </b-form>
  </div>
</template>

<script>
  import FractCalc from '@/components/fract-calc/FractCalc.vue';

  export default {
    name: 'FractCalcForm',
    components: {
      FractCalc
    },
    data () {
      return {
        errors: [],
        submit: false,
        fractions: {
          items: [{
              type: 'fraction',
              numerator: null,
              denominator: null
            },{
              type: 'operation',
              value: '+'
            },{
              type: 'fraction',
              numerator: null,
              denominator: null
            }
          ],
          result: null
        }
      }
    },
    methods: {
      checkForm (e) {
        let res = false;
        this.errors = [];
        if (!this.fractions.result) {
          this.errors.push('Заполните дроби');
          this.submit = false;
        } else {
          this.submit = true;
          this.errors = [];
        }
        res = this.errors.length
        e.preventDefault();
        return res;
      }
    }
  }
</script>
