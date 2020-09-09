<template>
  <section class="content-calculator">
    <div class="baseCalculator">
      <div class="painel">
        <h2>Calculadora</h2>
        <span class="calc">{{value}}</span>
        <span class="result">{{resultFunc}}</span>
      </div>

      <div class="numbers">
        <button v-for="(number) in numbers" :key="number" @click="numberFunc">{{number}}</button>
        <button key="=" @click="calcTotal">=</button>
      </div>

      <div class="operations">
        <button :key="apagar" @click="clearFunc">{{apagar}}</button>
        <button
          v-for="(operation) in operations"
          :key="operation"
          @click="operationFunc"
        >{{operation}}</button>
      </div>
      <button class="apagar-tudo" @click="clearAll">AC</button>
    </div>
  </section>
</template>

<script>
export default {
  name: "ContentCalculator",
  data() {
    return {
      numbers: ["7", "8", "9", "4", "5", "6", "1", "2", "3", "0", "."],
      operations: ["/", "*", "-", "+"],
      apagar: "<x",
      value: "",
      total: "",
    };
  },
  methods: {
    numberFunc({ target }) {
      this.value = this.value + target.innerText;
    },
    operationFunc({ target }) {
      this.value = String(this.value);
      if (parseFloat(this.value.substring(this.value.length - 1))) {
        this.value = this.value + target.innerText;
      } else if (
        this.value.substring(this.value.length - 1) !== target.innerText ||
        this.value.substring(this.value.length - 1) === "."
      ) {
        this.value = this.value.slice(0, -1) + target.innerText;
      }
    },
    calcTotal() {
      try {
        this.value = eval(this.value);
      } catch {
        console.log("Valor Invalido");
      }
    },
    clearFunc() {
      this.value = String(this.value);
      this.value = this.value.slice(0, -1);
    },
    clearAll() {
      this.value = "";
    },
  },
  computed: {
    resultFunc() {
      try {
        return eval(this.value);
      } catch {
        return "";
      }
    },
  },
};
</script>

<style scoped>
button {
  outline: none;
  border: none;
  cursor: pointer;
  transition: color 0.3s;
}
.baseCalculator {
  position: relative;
  max-width: 400px;
  margin: 36px auto 0px auto;
  background: var(--primary-color);
  display: grid;
  grid-template:
    "painel painel" 136px
    "number operations" 70vh
    / 1fr 120px;
}

.painel {
  grid-area: painel;
  background: #323232;
  padding-right: 16px;
}
.painel span {
  display: block;
}
.painel h2 {
  padding: 10px;
}
.painel .calc {
  text-align: right;
  font-size: 2rem;
}
.painel .result {
  text-align: right;
  font-size: 1.5rem;
  color: #919191;
  padding-top: 20px;
}

.numbers {
  grid-area: number;
}
.numbers button {
  width: 33.3%;
  height: 25%;
}
.numbers button,
.operations button {
  font-size: 2rem;
  background: var(--primary-color);
  transition: all 0.2s;
}
.operations {
  grid-area: operations;
}
.operations button {
  width: 100%;
  height: 20%;
  color: dodgerblue;
}
.apagar-tudo {
  position: absolute;
  width: 64px;
  height: 64px;
  top: 64px;
  left: 14px;
  border-radius: 5px;
  background: var(--primary-color);
  font-size: 1.5rem;
  transition: all 0.3s;
}

.apagar-tudo:focus {
  box-shadow: 0px 0px 0px 6px rgba(64, 64, 64, 0.8);
}
.numbers button:hover,
.operations button:hover,
.apagar-tudo:hover {
  background: #444;
}

@media screen and (max-width: 500px) {
  .baseCalculator {
    margin: 10px auto;
  }
}
@media screen and (max-width: 300px) {
  .baseCalculator {
    grid-template:
      "painel painel" 136px
      "number operations" 70vh
      / 1fr 80px;
  }
}
</style>