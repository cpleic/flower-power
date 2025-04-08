---
layout: default
title: Leaderboard Flores da Melhor Carrinha 
---


# 🏆 Top 10 Pételeiros (Fazedores de Pétalas duh)

<div id="leaderboard"></div>

<script>
  const sheetID = '14PnbkAb4wUjOORFmwI6ThG-WUsuDq6tdIMgSTexcs0o';
  const range = 'Leaderboard'; 
  const sheetURL = `https://sheets.googleapis.com/v4/spreadsheets/${sheetID}/values/${range}?key=AIzaSyDoUCZ4ZOdOZXy0OUGxGr5bW34VyqzP50U`;

  fetch(sheetURL)
    .then(response => response.json())
    .then(data => {
      // Remover o cabeçalho e garantir que temos uma lista de dados
      const entries = data.values.slice(1);
      
      // Ordena os dados pela pontuação (assumindo que a pontuação está na segunda coluna, índice 1)
      entries.sort((a, b) => b[1] - a[1]); // Ordena em ordem decrescente com base na pontuação

      // Pega apenas os 10 primeiros
      const top10Entries = entries.slice(0, 10);

      // Gerar a tabela HTML
      let tableHTML = '<table><tr><th>Posição</th><th>Nome do Pételeiro</th><th>Pontuação</th></tr>';

      top10Entries.forEach((entry, index) => {
        const nome = entry[0]; 
        const pontuacao = entry[1]; 
        tableHTML += `<tr><td>${index + 1}</td><td>${nome}</td><td>${pontuacao}</td></tr>`;
      });

      tableHTML += '</table>';
      document.getElementById('leaderboard').innerHTML = tableHTML;
    })
    .catch(error => console.error('Erro ao carregar os dados: ', error));
</script>
