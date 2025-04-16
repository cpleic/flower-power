---
layout: default
title: Leaderboard Flores da Melhor Carrinha 
---

# 🌸 **Flower Counter de LEIC** 🌸

## 🏆 Top 10 Pételeiros (Fazedores de Pétalas duh)

<audio id="bg-music" loop hidden>
  <source src="assets/Europe - The Final Countdown (Official Video).mp3" type="audio/mp3">
</audio>

<div class="container-geral">
  <img class="faixa-lateral esquerda" src="assets/noronhaClique.png" alt="Faixa Esquerda" />
  


<div id="leaderboard"></div>

<div id="contador" style=" background: #90E0EF; border-radius: 16px; font-size: 1.2em; box-shadow: 0 4px 12px rgba(0,0,0,0.1);"></div>




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
        <div style="margin-top: 30px; font-size: 1.3em; text-align: left;">
          <div style="margin-bottom: 10px;">
            ⏳ <strong>Faltam ${diasRestantes} dias</strong> para o glorioso Cortejo</strong>!
          </div>
          <div>
            🌼 <strong>Faltam ${faltamFlores} flores</strong> e 🌸 <strong>${faltamPetalas} pétalas</strong> para atingir o objetivo!
          </div>

          <div>
            🦨 Faltam <strong>12047348733242875639086359</strong> dias para os caloiros deixarem de ser <strong> burros </strong> 
          </div>

          
        </div>
      `;
      document.getElementById('contador').innerHTML = infoHTML;
    })
    .catch(error => console.error('Erro ao carregar os dados: ', error));


    window.addEventListener('click', () => {
    const audio = document.getElementById("bg-music");
    audio.play();
  }, { once: true });


</script>

<style>
  body {
    margin: 0;
    padding: 0;
    overflow-x: hidden;
    font-family: sans-serif;
  }

  .container-geral {
    display: flex;
    flex-direction: row;
    height: 100vh;
    width: 100vw;
  }

  .faixa-lateral {
    width: 200px;
    height: 100vh;
    object-fit: cover;
    flex-shrink: 0;
  }

  .esquerda {
    position: fixed;
    left: 0;
    top: 0;
  }

  .direita {
    position: fixed;
    right: 0;
    top: 0;
  }

  .conteudo-central {
    margin: 0 auto;
    padding: 40px 20px;
    max-width: 800px;
    z-index: 1;
    position: relative;
    background: white;
    min-height: 100vh;
  }

  #leaderboard, #contador {
    margin-top: 30px;
  }

  table {
    width: 100%;
    border-collapse: collapse;
    margin-top: 20px;
  }

  th, td {
    padding: 10px;
    border: 1px solid #ddd;
    text-align: center;
  }

  th {
    background-color: #f0f0f0;
  }
</style>

