<template>
    <div class="container">
        <div class="top">
            <h1>ConvertCoin</h1>
        </div>
        <div class="main">
            <div class="label">
                Você envia
            </div>
            <div class="coin1">
                <input type="number" class="inputCoin" v-model="coin1_value" v-on:input="calc" placeholder="insira o valor">
                <select name="coinIn" id="coinIn" class="coin" v-model="coin1" v-on:change="calc">
                    <option class="option" for="cointIn" value="BRL">BRL</option>
                    <option class="option" for="cointIn" value="USD">USD</option>
                    <option class="option" for="cointIn" value="EUR">EUR</option>
                </select>
            </div>
            <div class="info">
                <span><h5>{{demo}}</h5></span>
                <h5>IOF (1,10%) = {{iof_value}}</h5>
                <h5>Taxa administrativa (1,0%) = {{fx_value}}</h5>
            </div>
            <div class="label">
                Beneficiário recebe
            </div>
            <div class="coin2">
                <input type="text" class="inputCoin" v-model="coin2_value" disabled>
                <select name="coinOut" id="coinOut" class="coin" v-model="coin2" v-on:change="calc">
                    <option class="option" for="coinOut" value="USD">USD</option>
                    <option class="option" for="coinOut" value="EUR">EUR</option>
                    <option class="option" for="coinOut" value="BRL">BRL</option>
                </select>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data(){
        return{
            coin1_value: "",
            coin1: "BRL",
            coin2_value: 0,
            coin2: "USD",
            iof: 1.1,
            fx: 1,
            iof_value: "",
            fx_value: "",
            demo: "",
            valor_formatado: ""
        };
    },
    methods: {
        /*
            Os methods typeCoin1 e typeCoin2 foram foram criados apenas para teste
            do select. Mudando o v-on:change="calc" para "typeCoin1", vai mostrar
            no console que a o valor de coin1 está mudando corretamente.
        */
        typeCoin1(){
            /* console.log("Está chamando o typeCoin1!"); */
            console.log("Moeda 1 selecionada: ", this.coin1);
        },

        typeCoin2(){ //Vai setar o tipo da moeda de saida
            /* console.log("Está chamando o typeCoin2!"); */
            console.log("Moeda 2 selecionada: ", this.coin2);
        },

        calc(){
            /* console.log("Está chamando o calc!"); */
            /* console.log("Valor da moeda de entrada", this.coin1_value); */

            this.iof_value = ((this.coin1_value * this.iof) / 100).toFixed(2); //faz a porcentagem do IOF
            /* console.log("Valor do IOF sobre o valor",this.iof_value); */

            this.fx_value = ((this.coin1_value * this.fx) / 100).toFixed(2); //faz a porcentagem do FX
            /* console.log("Valor do FX sobre o valor", this.fx_value); */

            if (this.coin1 === "BRL" && this.coin2 === "USD"){ // BRL para USD
                this.coin2_value = (((this.coin1_value - this.iof_value) - this.fx_value) / 5.2164).toLocaleString('en-US', { style: 'currency', currency: 'USD' });
                this.demo = "1 BRL = 0.1917 USD";
            }
            
            if (this.coin1 === "BRL" && this.coin2 === "EUR"){ // BRL para EUR
                this.coin2_value = (((this.coin1_value - this.iof_value) - this.fx_value) / 6.3970).toLocaleString('de-DE', { style: 'currency', currency: 'EUR' });
                 this.demo = "1 BRL = 0,1563 EUR";
            }
            
            if (this.coin1 === "USD" && this.coin2 === "BRL"){ // USD para BRL
                this.coin2_value = (((this.coin1_value - this.iof_value) - this.fx_value) * 5.2164).toLocaleString('pt-BR', { style: 'currency', currency: 'BRL' });
                this.demo = "1 USD = 5.2164 BRL";
            }
            
            if (this.coin1 === "USD" && this.coin2 === "EUR"){ // USD para EUR
                this.coin2_value = (((this.coin1_value - this.iof_value) - this.fx_value) / 1.2206).toLocaleString('de-DE', { style: 'currency', currency: 'EUR' });
                this.demo = "1 USD = 0.8192 EUR";
            }
            
            if (this.coin1 === "EUR" && this.coin2 === "USD"){ // EUR para USD
                this.coin2_value = (((this.coin1_value - this.iof_value) - this.fx_value) * 1.2206).toLocaleString('en-US', { style: 'currency', currency: 'USD' });
                this.demo = "1 EUR = 1.2206 USD";
            }

            if (this.coin1 === "EUR" && this.coin2 === "BRL"){ // EUR para BRL
                this.coin2_value = (((this.coin1_value - this.iof_value) - this.fx_value) * 6.3970).toLocaleString('pt-BR', { style: 'currency', currency: 'BRL' });
                this.demo = "1 EUR = 6.3970 BRL";
            }

            if (this.coin1 === "BRL" && this.coin2 === "BRL"){ // BRL pada BRL
                this.coin2_value = (((this.coin1_value - this.iof_value) - this.fx_value) * 1).toLocaleString('pt-BR', { style: 'currency', currency: 'BRL' });
                this.demo = "1 BRL = 1 BRL";
            }

            if (this.coin1 === "USD" && this.coin2 === "USD"){ // USD para USD
                this.coin2_value = (((this.coin1_value - this.iof_value) - this.fx_value) * 1).toLocaleString('en-US', { style: 'currency', currency: 'USD' });
                this.demo = "1 USD = 1 USD";
            }

            if (this.coin1 === "EUR" && this.coin2 === "EUR"){ // EUR para EUR
                this.coin2_value = (((this.coin1_value - this.iof_value) - this.fx_value) * 1).toLocaleString('de-DE', { style: 'currency', currency: 'EUR' });
                this.demo = "1 EUR = 1 EUR";
            }
        }
    }

};
</script>

<style scoped>
    html {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
    }
    .container {
        width: 100%;
        height: 100%;

        font-family: Helvetica, sans-serif;
        font-size: 16px;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        justify-content: center;
        color: #0e1c36;
    }

    .top {
        width: 100%;
        height: 6rem;
        padding-top: 1.5rem;
        padding-bottom: 1.5rem;

        font-size: 1.2rem;
        color: #f9fbf2;
        background-color: #14213d;
        align-items: center;

        box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.5);
    }

    .main {
        margin: auto;
        width: 25rem;
        height: 100%;
        padding-top: 2rem;
        padding-bottom: 1.5rem;
    }

    .label {
        font-size: 1.2rem;
        font-weight: 500;
        text-align: left;
        color: #0a111f;
        padding-left: 0.5rem;
        margin-bottom: 0.3rem;
    }

    .coin1 {
        width: 100%;
        height: auto;
    }

    .inputCoin {
        width: 60%;
        height: 4rem;
        border: 1px solid #e5e5e5;
        border-radius: 3px;
        outline: none;
        font-size: 1.2rem;
        margin-right: 0.5rem;
        padding-left: 1rem;
        transition: 300ms;
    }

    .inputCoin:focus {
        border: 1px solid #4895ef;
    }

    .inputCoin:active {
        border: 1px solid #4895ef;
        outline: none;
    }

    .inputCoin::placeholder {
        font-size: 1.1rem;
        outline: none;
    }

    .coin {
        width: 30%;
        height: 4rem;
        appearance: none;
        align-items: center;
        text-align: center;
        justify-content: center;
        font-size: 1.2rem;
        color: #0a111f;
        border: 1px solid #e5e5e5;
        border-radius: 3px;
        background-color: #457b9d;
        color: #FFF;
        transition: 400ms;
    }

    .coin:hover {
        background-color: #e5e5e5;
        border: 1px solid #4895ef;
        color: #14213d;
        transition: 400ms;
        outline: none;
    }

    .coin:active {
        background-color: #e5e5e5;
        color: #14213d;
        transition: 400ms;
        outline: none;
    }

    .coin:focus {
        background-color: #e5e5e5;
        color: #14213d;
        transition: 400ms;
        outline: none;
    }

    .info {
        font-size: 1rem;
        font-weight: 500;
        text-align: left;
        color: #6d6875;
        padding-left: 0.5rem;
        margin-bottom: 0.3rem;
    }

</style>