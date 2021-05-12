<template>
  
<div class="content" role="main">
  <h1>IMC</h1>
  <form v-on:click.prevent="calcular">
    <div class="form-group">
      <label for="">Altura</label>
      <input type="number" v-model="altura" class="form-control">          
    </div>
    <div class="form-group">      
      <label for="">Peso</label>
      <input type="number" v-model="peso" class="form-control">
    </div>
    <button type="submit" class="btn btn-primary">Calcular</button>    
  </form>
  <div class="Resultado">
    <h2>
      IMC: {{resultado | formatedResultado}}
      
    </h2>
    <table class="table-calc" cellspacing="0">     
      <thead>        					
        <tr class="table-calc-blue">
          <th>IMC</th>
          <th>Classificação</th>
          <th style="text-align: center">Obesidade <small>(grau)</small></th>
        </tr>  
      </thead>
      <tbody>	      
        <tr v-bind:class="{ 'resultado' : resultado < 18.5 && resultado > 0}" >
          <td>Menor que 18,5</td>
          <td>Magreza</td>
          <td style="text-align: center">0</td>
        </tr>
        
        <tr v-bind:class="{ 'resultado' :  resultado < 25 && resultado >= 18.5}" >
          <td>Entre 18,5 e 24,9</td>
          <td>Normal</td>
          <td style="text-align: center">0</td>
        </tr>
        
        <tr v-bind:class="{ 'resultado' :  resultado < 30 && resultado >= 25}" >
          <td>Entre 25,0 e 29,9</td>
          <td>Sobrepeso</td>
          <td style="text-align: center">I</td>
        </tr>
        
        <tr v-bind:class="{ 'resultado' :  resultado < 40 && resultado >= 30}" >
          <td>Entre 30,0 e 39,9</td>
          <td>Obesidade</td>
          <td style="text-align: center">II</td>
        </tr>

        <tr v-bind:class="{ 'resultado' : resultado >= 40 }" >
          <td>Maior que 40,0</td>
          <td>Obesidade Grave</td>
          <td style="text-align: center">III</td>
        </tr>
      </tbody>

    </table>
  </div>
</div>
</template>

<script>
    export default {
        name: 'IMC',
        data(){
            return {
                resultado: Number,   
                altura: Number,
                peso: Number
            }
        },
        methods: {
            calcular(){
                let altura = this.altura /100;
                this.resultado = this.peso / (altura * altura);
            }
        },
        filters: {
            formatedResultado: function(value){
                if(isNaN(value)){
                    return 0
                }
                return Number(value).toFixed(2)
            }
        }
    }
</script>
<style scoped>
    .content {
        display: flex;
        margin: 82px auto 32px;
        padding: 0 16px;
        max-width: 960px;
        flex-direction: column;
        align-items: center;
    }
    table {
        width: 500px;
    }
    .resultado{
        background-color: lightgreen;
    }
</style>
