<template>
  <div class="converter">
  <button class="button-converter" @click="converter">Converter valor</button>
      <div class="from">
     
      <p class="messege-info" v-if=" hasValueFrom">Escolha as moedas para digitar o valor</p>
          <p>{{itemFrom.name}}</p>
          <input type="number" placeholder="Valor" v-model="value" >
          <p>{{itemFrom.initials}}</p>
      </div>
      <div class="for">
        
        <p>{{itemFor.name}}</p>
        <p class="messege-info" v-if=" hasValueFor">Escolha a moeda que quer converter</p>
        <p class="value">{{itemFor.symbol}}{{moedaatual}}</p>
        
        <p>{{itemFor.initials}}</p>
      </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
    name: "Converter",
       data() {
        return {
            price: [],
            moedaatual: '',
            value: '',
            ChosenCurrency: "",
            hasValueFrom: true,
            hasValueFor: true,
            currencyError: false
        }
    },
    props: {
        itemFrom: Object,
        itemFor: Object
    },
    watch: {
        itemFrom() {
            this.hasValueFrom = false;
        },
        itemFor() {
            this.hasValueFor = false;
        },
    },
    methods: {
        converter() {
          axios.get(`https://economia.awesomeapi.com.br/last/${this.itemFrom.initials}-${this.itemFor.initials}`).then(response => {
            this.ChosenCurrency = `${this.itemFrom.initials}${this.itemFor.initials}`   
          switch (this.ChosenCurrency) {
              case 'BRLUSD':
                  this.price = response.data.BRLUSD.bid;
                  break;
                case 'BRLEUR':
                  this.price = response.data.BRLEUR.bid;
                break;
                 case 'BRLGBP':
                  this.price = response.data.BRLGBP.bid;
                break;
                 case 'USDBRL':
                  this.price = response.data.USDBRL.bid;
                  break;
                case 'USDEUR':
                  this.price = response.data.USDEUR.bid;
                break;
                 case 'USDGBP':
                  this.price = response.data.USDGBP.bid;
                break;
                case 'EURUSD':
                  this.price = response.data.EURUSD.bid;
                  break;
                case 'EURBRL':
                  this.price = response.data.EURBRL.bid;
                break;
                 case 'EURGBP':
                  this.price = response.data.EURGBP.bid;
                break;
                 case 'GBPUSD':
                  this.price = response.data.GBPUSD.bid;
                  break;
                case 'GBPBRL':
                  this.price = response.data.GBPBRL.bid;
                break;
                 case 'GBPEUR':
                  this.price = response.data.GBPEUR.bid;
                break;
          }
            this.ConvertCurrency();
           
            
        })
        },
        ConvertCurrency() {
            if(this.value.length == 0) return
            this.moedaatual = (this.price * parseFloat(this.value)).toFixed(2);
            this.moedaatual = this.moedaatual.toString().replace(".",",")
        },
    }
}
</script>

<style scoped lang="less">
.converter {
    width: 500px;
    height: 380px;
    margin: auto;

    p {
        margin: 0;
    }


    .from {
        height: 190px;
        background: @pink;
        display: flex;
        flex-direction: column;
        justify-content: space-around;
        align-items: center;

        border-radius: 8px 8px 0 0;

        p {
            color: @light-pink;
            font-size: 1.6rem;
            font-weight: 300;
        }

        .messege-info{
        padding: 10px;
        font-size: 1.5rem;

    }

        input {
            border: none;
            text-align: center;
            outline: none;
            padding: 5px 8px;
            border-radius: 8px;
            color: @pink;
            font-weight: 500;
            font-size: 1.2rem;

            &::placeholder {
                color: @pink;
            }
        }
    }

    .for {
        background: white;
        height: 190px;
        border-radius:0 0 8px 8px;
        display: flex;
        flex-direction: column;
        justify-content: space-around;
        align-items: center;

        p{
            color: @pink;
            font-size: 1.6rem;
            font-weight: 300;
        }

    
    }
       .button-converter {
           display:block;
           margin: 30px auto;
           background: @pink;
            border: none;
            outline: none;
            padding: 8px 30px;
            border-radius: 8px;
            color: #fff;
            font-size: 1.1rem;
            font-weight: 500;
    
        }

        @media @smartphones {
            width: 350px;

            .from {
                .messege-info {
                    font-size: 1rem
                }
            }

             .for {
                .messege-info {
                    font-size: 1rem
                }
            }
        }

        
 
}

</style>
