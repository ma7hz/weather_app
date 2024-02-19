// Chave de acesso à API
const key = "a1a346676d473a21b005c651cdf37107";

// Função para colocar os dados na tela
function colocarDadosNaTela(dados) {
    console.log(dados);
    document.querySelector(".cidade").innerHTML = "Tempo em " + dados.name;
    document.querySelector(".temp").innerHTML = Math.floor(dados.main.temp) + "ºC";
    document.querySelector(".texto-previsao").innerHTML = dados.weather[0].description;
    document.querySelector(".umidade").innerHTML = dados.main.humidity + "%";
    document.querySelector(".img-previsao").src = `https://openweathermap.org/img/wn/${dados.weather[0].icon}.png`;
}

// Função assíncrona para buscar os dados da cidade
async function buscarCidade(cidade) {
    // Realiza uma requisição assíncrona para a API do OpenWeatherMap
    const dados = await fetch(`https://api.openweathermap.org/data/2.5/weather?q=${cidade}&appid=${key}&lang=pt_br&units=metric`)
                            .then(Resposta => Resposta.json());

    // Chama a função para colocar os dados na tela com os dados obtidos da API
    colocarDadosNaTela(dados);
}

// Função chamada quando o botão é clicado
function cliqueiNoBotao() {
    // Obtém o valor da cidade digitado pelo usuário
    const cidade = document.querySelector(".input-cidade").value;

    // Chama a função para buscar os dados da cidade
    buscarCidade(cidade);
}
