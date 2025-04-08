---
layout: default
title: Leaderboard Flores da Melhor Carrinha 
---


# 🏆 Top 10 Pételeiros (Fazedores de Pétalas duh)

<ul id="leaderboard"></ul>


  <script>
    const sheetId = '14PnbkAb4wUjOORFmwI6ThG-WUsuDq6tdIMgSTexcs0o';
    const url = `https://spreadsheets.google.com/feeds/list/14PnbkAb4wUjOORFmwI6ThG-WUsuDq6tdIMgSTexcs0o/od6/public/values?alt=json`;

    fetch(url)
      .then(res => res.json())
      .then(data => {
        const entries = data.feed.entry;
        const leaderboard = document.getElementById('leaderboard');

        const players = entries.map(entry => ({
          name: entry.gsx$name.$t,
          score: parseInt(entry.gsx$score.$t)
        }));

        // Ordena e mostra os 10 primeiros
        players.sort((a, b) => b.score - a.score).slice(0, 10).forEach(player => {
          const li = document.createElement('li');
          li.textContent = `${player.name} - ${player.score} pontos`;
          leaderboard.appendChild(li);
        });
      });
  </script>
