<template>
  <h1>BMI Calculator</h1>
  <div class="main-content">
    <div class="calculator-section">
      <div class="div-imc">
        <span class="p-float-label">
          <InputText id="input-weight" type="text" v-model="weight" :disabled="imc"/>
          <label for="input-weight">Weight</label>
        </span>
      </div>
      
      <div class="div-imc">
        <span class="p-float-label">
          <InputMask id="input-height" type="text" v-model="height" mask="9.99" :disabled="imc"/>
          <label for="input-height">Height</label>
        </span>
      </div>
  
      <div class="div-imc" v-if="!imc">
        <Button label="Calculate" @click="calculate" class="btn-calculate"/>
        <!-- <Button label="Limpar" @click="clear"></Button> -->
      </div>
      <div class="div-imc" v-show="imc">
        <Button label="Recalculate" @click="clear" class="btn-calculate"/>
      </div>
    </div>  
    <div class="result-section">
      <p class="p-title"><strong>RESULTS</strong></p>
      <div class="results" v-if="imc">
        <p class="p-text">BMI:</p>
        <p class="label-result">{{imc}} </p>
      </div>
      <div class="results" v-if="imc">
        <p class="p-text">Classification:</p>
        <p class="label-result">{{classification}} </p>
      </div>
    </div>
    <!-- <div class="result-section" v-if="imc">
      <p class="label-result" >Seu IMC é: {{imc}} </p>
      <p class="label-classification">A classificação do seu IMC é: {{classification}} </p>
      <Button @click="clear" label="Calcular novamente" ></Button>
    </div> -->
  </div>


</template>

<script>
export default {
    data() {
      return {
        height: null,
        weight: null,
        imc: null,
        classification: ""
      }
    },
    methods: {
      calculate() {
        this.imc = (this.weight / (this.height * this.height)).toFixed(2);
        if (this.imc < 18.5) {
          this.classification = "Underweight";
        } else if (this.imc >= 18.5 && this.imc < 25) {
          this.classification = "Normal";
        } else if (this.imc >= 25 && this.imc < 30) {
          this.classification = " Overweight";
        } else if (this.imc >= 30 && this.imc < 40) {
          this.classification = "Obesity";
        } else if (this.imc >= 40){
          this.classification = "Severe Obesity";
        } else {
          this.classification = "Invalid"
        }
      },
      clear() {
        this.height = null;
        this.weight = null;
        this.imc = null;
        this.result = null;
        this.classification = null;
      }
    }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Open+Sans:wght@300;400;500;700&display=swap');

body {
  background-color: #C5E4E7;
  font-family: 'Open Sans', sans-serif;
  display: flex;
  justify-content: center;
  align-content: center;
}

h1 {
  text-align: center;
  color: #00474B;
  margin: 60px;
}

.main-content {
  background-color: #FFFFFF;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 600px;
  height: 260px;
  border-radius: 10px;
}

.calculator-section {
  margin-top: 30px;
  margin-bottom: 30px;
  margin-right: 30px;
}

.div-imc {
  margin-top: 2rem;
}

.btn-calculate {
   width: 230px;
}

Button {
  background-color: #1fb19d !important;
  border-color: #1fb19d !important;
}

.result-section {
  /* display: flex;
  flex-direction: column;
  justify-content: center; */
  background-color: #00474B;
  color: #FFFFFF;
  width: 250px;
  height: 220px;
  border-radius: 5px;
  opacity: 80%;
}

.p-title {
  text-align: center;
}

.results {
  padding-left: 15px;
}

.p-text {
  margin-top: 1px;
  margin-bottom: 3px;
}

.label-result {
  margin-top: 0;
  margin-bottom: 15px;
  font-size: 1.7rem;
}
</style>
