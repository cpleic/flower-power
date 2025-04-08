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
      const entries = data.values;

      const leaderboardData = entries.slice(1).filter(row => row[0] && !isNaN(row[1]));
      leaderboardData.sort((a, b) => b[1] - a[1]);
      const top10 = leaderboardData.slice(0, 10);

      let html = '<table><tr><th>Posição</th><th>Nome do Pételeiro</th><th>Pontuação</th></tr>';
      top10.forEach((row, i) => {
        html += `<tr><td>${i + 1}</td><td>${row[0]}</td><td>${row[1]}</td></tr>`;
      });
      html += '</table>';
      document.getElementById('leaderboard').innerHTML = html;

      const faltamPetalas = entries[1][5]; // F2
      const faltamFlores = entries[1][6];  // G2

      const hoje = new Date();
      const vinteMaio = new Date(hoje.getFullYear(), 4, 20);
      if (hoje > vinteMaio) vinteMaio.setFullYear(vinteMaio.getFullYear() + 1);
      const diasRestantes = Math.ceil((vinteMaio - hoje) / (1000 * 60 * 60 * 24));

      const infoHTML = `
        <div style="margin-top: 30px; font-size: 1.3em; text-align: center;">
          <div style="margin-bottom: 10px;">
            ⏳ <strong>Faltam ${diasRestantes} dias</strong> para o glorioso dia <strong>20 de maio</strong>!
          </div>
          <div>
            🌼 <strong>${faltamFlores} flores</strong> e 🌸 <strong>${faltamPetalas} pétalas</strong> para atingir o objetivo!
          </div>
        </div>
      `;
      document.getElementById('contador').innerHTML = infoHTML;
    })
    .catch(error => console.error('Erro ao carregar os dados: ', error));
</script>


<style>
  header, .header, .page-header {
    display: none;
  }
</style>
