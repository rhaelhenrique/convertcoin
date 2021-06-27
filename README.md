# ConvertCoin
Calculadora para conversão de moedas

##### Resumo
    O usuário pode inserir qualquer valor, escolher a moeda para o valor inserido e outra moeda para conversão.
    A calculadora então deverá exibir as taxas e o valor convertido.


##### A calculadora deverá funcionar com 3 moedas:
    BRL -> Real
    USD -> Dolar
    EUR -> Euro

##### Duas taxas devem ser deduzidas em todas as operações:
    IOF: 1.1%
    FX: 1.0%

##### Considerar as seguintes taxas de conversão (fx_rate):
    USD -> BRL: 5.2164
    EUR -> BRL: 6.3970
    EUR -> USD: 1.2206


##### Formula do cálculo:
    converted_value = (value - iof_value - fx_value) * fx_rate

##### Onde:
    iof_value = 1.1% do valor a ser convertido
    fx_value = 1% do valor a ser convertido
    fx_rate = taxa de câmbio

##### Exemplo de cálculo para 1000 USD sendo convertido para BRL:
    iof_value = 11.0
    fx_value = 10.0
    fx_rate = 5.2164
    converted_value = 5106.8556

##### Projeto feito em Vue.js
    Autor: Rhael Henrique

##### Disponível na plataforma Vercel: https://convertcoin.vercel.app/

##### Info:
    1) Escolha BRL, USD ou EUR, para os valores de entrada e saída (BRL -> USD é a seleção default);
    2) Insira o valor de entrada.
    > O resultado será apresentado automaticamente.
