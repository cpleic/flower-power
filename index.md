---
layout: default
title: Leaderboard Flores da Melhor Carrinha 
---

# 🌸 Flower Counter de LEIC 🌸

## 🏆 Top 10 Pételeiros (Fazedores de Pétalas duh)

<div id="leaderboard"></div>

<script>
  const sheetID = '14PnbkAb4wUjOORFmwI6ThG-WUsuDq6tdIMgSTexcs0o';
  const range = 'Leaderboard'; 
  const sheetURL = `https://sheets.googleapis.com/v4/spreadsheets/${sheetID}/values/${range}?key=AIzaSyDoUCZ4ZOdOZXy0OUGxGr5bW34VyqzP50U`;
  
  
  fetch(sheetURL)
    .then(response => response.json())
    .then(data => {

      
      const entries = data.values.slice(1);
                  
      entries.sort((a, b) => b[1] - a[1]); 

      const top10Entries = entries.slice(0, 10);

      let tableHTML = '<table><tr><th>Posição</th><th>Nome do Pételeiro</th><th>Pétalas</th></tr>';

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

<style>
  header, .header, .page-header {
    display: none;
  }
</style>
