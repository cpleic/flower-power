---
layout: default
title: Leaderboard Flores da Melhor Carrinha 
---

# 🏆 Top 10 Pételeiros (Fazedores de Pétalas duh)

<ul id="leaderboard">A enrolar...</ul>

<script>
  const sheetId = '2PACX-1vTkxv4bxLhdbY-5rV0wRPbUMMNuzNkeqKTOORnVCfoYwdFxfBu7UlOe9k7RAEhSE2AiUv1PYgviJI6m'; // substitui com o ID da tua sheet
  const url = `https://docs.google.com/spreadsheets/d/e/2PACX-1vTkxv4bxLhdbY-5rV0wRPbUMMNuzNkeqKTOORnVCfoYwdFxfBu7UlOe9k7RAEhSE2AiUv1PYgviJI6m/pubhtml`;

  fetch(url)
    .then(res => res.json())
    .then(data => {
      const entries = data.feed.entry;
      const leaderboard = document.getElementById('leaderboard');
      leaderboard.innerHTML = ''; // limpa o "A carregar..."

      const players = entries.map(entry => ({
        name: entry.gsx$name.$t,
        score: parseInt(entry.gsx$score.$t)
      }));

      players.sort((a, b) => b.score - a.score).slice(0, 10).forEach(player => {
        const li = document.createElement('li');
        li.textContent = `${player.name} – ${player.score} pontos`;
        leaderboard.appendChild(li);
      });
    });
</script>
