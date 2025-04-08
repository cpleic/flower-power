---
layout: default
title: Leaderboard Flores da Melhor Carrinha 
---


# 🏆 Top 10 Pételeiros (Fazedores de Pétalas duh)

<div id="leaderboard"></div>

<script>
  const sheetID = '2PACX-1vTkxv4bxLhdbY-5rV0wRPbUMMNuzNkeqKTOORnVCfoYwdFxfBu7UlOe9k7RAEhSE2AiUv1PYgviJI6m';
  const range = 'Leaderboard'; 
  const sheetURL = `https://sheets.googleapis.com/v4/spreadsheets/${sheetID}/values/${range}?key=YOUR_API_KEY`;

  fetch(sheetURL)
    .then(response => response.json())
    .then(data => {
      const entries = data.values.slice(1, 11); 
      let tableHTML = '<table><tr><th>Posição</th><th>Nome do Pételeiro</th><th>Pontuação</th></tr>';

      entries.forEach((entry, index) => {
        const nome = entry[0]; /
        const pontuacao = entry[1]; 
        tableHTML += `<tr><td>${index + 1}</td><td>${nome}</td><td>${pontuacao}</td></tr>`;
      });

      tableHTML += '</table>';
      document.getElementById('leaderboard').innerHTML = tableHTML;
    })
    .catch(error => console.error('Erro ao carregar os dados: ', error));
</script>
