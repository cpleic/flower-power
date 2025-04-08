---
layout: default
title: Leaderboard Flores da Melhor Carrinha 
---


# 🏆 Top 10 Pételeiros (Fazedores de Pétalas duh)

<script>
  const sheetID = '2PACX-1vTkxv4bxLhdbY-5rV0wRPbUMMNuzNkeqKTOORnVCfoYwdFxfBu7UlOe9k7RAEhSE2AiUv1PYgviJI6m';
  const sheetGID = '0'; 
  const sheetURL = `https://spreadsheets.google.com/feeds/list/${sheetID}/${sheetGID}/public/values?alt=json`;

  fetch(sheetURL)
    .then(response => response.json())
    .then(data => {
      const entries = data.feed.entry;
      const leaderboard = entries.slice(0, 10); 
      let tableHTML = '<table><tr><th>Posição</th><th>Nome</th><th>Pétalas</th></tr>';

      leaderboard.forEach((entry, index) => {
        const nome = entry['gsx$name'].$t; 
        const pontuacao = entry['gsx$soma'].$t; 
        tableHTML += `<tr><td>${index + 1}</td><td>${nome}</td><td>${pontuacao}</td></tr>`;
      });

      tableHTML += '</table>';
      document.getElementById('leaderboard').innerHTML = tableHTML;
    })
    .catch(error => console.error('Erro ao carregar os dados: ', error));
</script>
