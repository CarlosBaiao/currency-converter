<template>
  <div class="currency-type">
    <div class="type-container">
       <div class="options-type">
      <label for="from">De</label>
      <select id="from" v-model="currencyFrom">
        <option v-for="type in currency" :key="type.id" :value="type">
          {{ type.name}}
        </option>
      </select>
    </div>
      <div class="options-type">
      <label for="for">Para</label>
      <select id="for" v-model="currencyFor" >
        <option v-for="type in currency" :key="type.id" :value="type">
          {{ type.name}}
        </option>
      </select>
    </div>
    </div>
    <Converter :itemFrom="currencyFrom" :itemFor="currencyFor"/>
  </div>
</template>

<script>
import Converter  from "./Converter.vue";
export default {
  name: "CurrencyType",
  components: {
    Converter
  },
  data() {
    return {
      currency: [
        { initials: "USD", name: "Dólar", symbol: "US$" , id: 1 },
        { initials: "BRL", name: "Real", symbol: "R$", id: 2 },
        { initials: "EUR", name:"Euro", symbol: "€" ,id: 3 },
        { initials: "GBP", name: "Libra", symbol:"£", id: 5 },
      ],
      currencyFrom: "",
      currencyFor: ""
    };
    
  },
};
</script>

<style scoped lang="less">
.currency-type {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
 

  .type-container {
    display: flex;
  justify-content: center;
  align-items: center;
  width: 500px;
  margin: auto;
  }
  
  .options-type {
    margin: 40px;
    height: 90px;
    width: 200px;
    display: flex;
    justify-content: center;
    align-items: center;

    label {
      color: @pink;
      font-size: 2rem;
      padding-right: 10px;
    }

    select {
      width: 120px;
      height:30px;
      border: none;
      border-radius: 8px;
      outline: none;
      text-align: center;
      color: @pink;
    }
  }

  @media @smartphones {
     .type-container {
       width: 350px;
     }


       .options-type {
         width: 140px;

         label {
           font-size: 1.2rem;
         }
       }

  }
}
</style>
