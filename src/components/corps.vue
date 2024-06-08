<template>
  <div class="corps">
    <h1>Calculatrice</h1>
    <div class="ecran">
      <p>{{ ecran }}</p>
    </div>
    <div class="boutons">
      <button @click="clearEcran">C</button>
      <button @click="deleteNumber">DEL</button>
      <button @click="operation('%')">%</button>
      <button @click="operation('/')" class="operateur">/</button>
      <button @click="ecrireNombre(7)">7</button>
      <button @click="ecrireNombre(8)">8</button>
      <button @click="ecrireNombre(9)">9</button>
      <button @click="operation('*')" class="operateur">*</button>
      <button @click="ecrireNombre(4)">4</button>
      <button @click="ecrireNombre(5)">5</button>
      <button @click="ecrireNombre(6)">6</button>
      <button @click="operation('-')" class="operateur">-</button>
      <button @click="ecrireNombre(1)">1</button>
      <button @click="ecrireNombre(2)">2</button>
      <button @click="ecrireNombre(3)">3</button>
      <button @click="operation('+')" class="operateur">+</button>
      <button @click="ecrireNombre(0)" class="wide">0</button>
      <button @click="ecrireNombre('.')">.</button>
      <button @click="calculate" class="operateur">=</button>
      <button @click="operation('^')" class="operateur">x^y</button>
      <button @click="sqrt" class="operateur">√</button>
    </div>
  </div>
</template>

<script>
import { evaluate } from 'mathjs';

export default {
  name: 'CalculatriceVuejs',
  data() {
    return {
      ecran: '',
      precedent: '',
      action: null,
    };
  },
  methods: {
    ecrireNombre(nb) {
      if (this.ecran === '0') {
        this.ecran = String(nb);
      } else {
        this.ecran += String(nb);
      }
    },
    operation(op) {
      if (this.ecran !== '') {
        this.ecran += op;
      }
    },
    deleteNumber() {
      this.ecran = this.ecran.slice(0, -1);
    },
    clearEcran() {
      this.ecran = '';
    },
    calculate() {
      try {
        this.ecran = String(evaluate(this.ecran));
      } catch (error) {
        this.ecran = 'ERROR';
      }
    },
    sqrt() {
      try {
        this.ecran = String(Math.sqrt(Number(this.ecran)));
      } catch (error) {
        this.ecran = 'ERROR';
      }
    }
  },
};
</script>
