<!DOCTYPE html>
<html>
<head>
  <title>Scopa — Carte Napoletane 🃏</title>
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; font-family: Arial; }
    body {
      background: #006633;
      color: white;
      text-align: center;
      padding: 20px;
      min-height: 100vh;
    }
    h1 { margin-bottom: 20px; font-size: 28px; }
    .mazzo { margin-bottom: 15px; font-size: 16px; }
    .zona { margin: 25px auto; max-width: 800px; }
    .zona h2 { margin-bottom: 10px; font-size: 18px; opacity: 0.9; }

    /* Stile carta napoletana */
    .carta {
      width: 90px;
      height: 140px;
      background: #fff;
      border-radius: 8px;
      display: inline-block;
      margin: 8px;
      padding: 8px;
      color: #1a1a1a;
      font-weight: bold;
      box-shadow: 3px 3px 6px rgba(0,0,0,0.3);
      position: relative;
      cursor: pointer;
      transition: transform 0.2s;
    }
    .carta:hover { transform: translateY(-5px); }

    /* Colori per seme */
    .denari { color: #b8860b; border-left: 6px solid #b8860b; }
    .coppe  { color: #c00; border-left: 6px solid #c00; }
    .spade  { color: #222; border-left: 6px solid #222; }
    .bastoni{ color: #3b6e22; border-left: 6px solid #3b6e22; }

    .valore { font-size: 22px; position: absolute; top: 8px; left: 8px; }
    .seme   { font-size: 30px; position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%); }
    .valore-basso { font-size: 22px; position: absolute; bottom: 8px; right: 8px; transform: rotate(180deg); }

    .punteggio { margin-top: 20px; font-size: 20px; font-weight: bold; }
    button {
      background: #fff;
      color: #006633;
      border: none;
      padding: 10px 20px;
      font-size: 16px;
      border-radius: 6px;
      cursor: pointer;
      margin: 10px;
      font-weight: bold;
    }
    button:hover { background: #f0f0f0; }
  </style>
</head>
<body>

  <h1>🃏 LA SCOPA — Carte Napoletane</h1>
  <div class="mazzo" id="infoMazzo">Carte nel mazzo: 40</div>
  <button onclick="nuovaPartita()">🔄 Nuova Partita</button>

  <div class="punteggio">
    Tu: <span id="mieiPunti">0</span> — Avversario: <span id="suoiPunti">0</span>
  </div>

  <!-- TAVOLO -->
  <div class="zona">
    <h2>📍 Tavolo</h2>
    <div id="tavolo"></div>
  </div>

  <!-- MANO TUO -->
  <div class="zona">
    <h2>✋ Tua mano</h2>
    <div id="manoGiocatore"></div>
  </div>

  <script>
    // Dati del mazzo napoletano
    const semi = [
      { nome: 'denari', simbolo: '🪙', classe: 'denari' },
      { nome: 'coppe', simbolo: '🏆', classe: 'coppe' },
      { nome: 'spade', simbolo: '⚔️', classe: 'spade' },
      { nome: 'bastoni', simbolo: '🌿', classe: 'bastoni' }
    ];
    const valori = [
      { numero: 1, nome: 'Asso', punteggio: 1 },
      { numero: 2, nome: '2', punteggio: 2 },
      { numero: 3, nome: '3', punteggio: 3 },
      { numero: 4, nome: '4', punteggio: 4 },
      { numero: 5, nome: '5', punteggio: 5 },
      { numero: 6, nome: '6', punteggio: 6 },
      { numero: 7, nome: '7', punteggio: 7 },
      { numero: 8, nome: 'Fante', punteggio: 8 },
      { numero: 9, nome: 'Cavallo', punteggio: 9 },
      { numero: 10, nome: 'Re', punteggio: 10 }
    ];

    let mazzo = [];
    let manoGiocatore = [];
    let manoAvversario = [];
    let tavolo = [];
    let puntiGiocatore = 0;
    let puntiAvversario = 0;

    // Crea mazzo
    function creaMazzo() {
      mazzo = [];
      for (let s of semi) {
        for (let v of valori) {
          mazzo.push({ seme: s, valore: v });
        }
      }
      // Mescola
      for (let i = mazzo.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [mazzo[i], mazzo[j]] = [mazzo[j], mazzo[i]];
      }
    }

    function cartaHTML(carta) {
      return `
        <div class="carta ${carta.seme.classe}">
          <div class="valore">${carta.valore.nome}</div>
          <div class="seme">${carta.seme.simbolo}</div>
          <div class="valore-basso">${carta.valore.nome}</div>
        </div>
      `;
    }

    function aggiornaSchermo() {
      document.getElementById('tavolo').innerHTML = tavolo.map(cartaHTML).join('');
      document.getElementById('manoGiocatore').innerHTML = manoGiocatore.map(cartaHTML).join('');
      document.getElementById('infoMazzo').textContent = `Carte nel mazzo: ${mazzo.length}`;
      document.getElementById('mieiPunti').textContent = puntiGiocatore;
      document.getElementById('suoiPunti').textContent = puntiAvversario;
    }

    function distribuisci() {
      manoGiocatore = mazzo.splice(0, 3);
      manoAvversario = mazzo.splice(0, 3);
      tavolo = mazzo.splice(0, 4);
    }

    function nuovaPartita() {
      puntiGiocatore = 0;
      puntiAvversario = 0;
      creaMazzo();
      distribuisci();
      aggiornaSchermo();
    }

    // Avvio automatico
    nuovaPartita();
  </script>

</body>
</html>

🎮 Come usarlo:
Copia tutto il codice
Apri il Blocco Note
Incolla → Salva come scopa-napoletana.html
Aprilo nel browser: vedrai subito il mazzo vero! 🃏✨
📌 Cosa c'è adesso:
✅ Tutti e 4 i semi napoletani con i colori giusti
✅ Carte dall'Asso al Re (40 totali)
✅ Mazzo mescolato casualmente ad ogni partita
✅ Distribuzione iniziale: 3 in mano, 4 sul tavolo
✅ Pulsante per ricominciare
🚀 Prossimi passi:
Giocare una carta → prendere dal tavolo
Regola della Scopa 🧹
Conteggio punti alla fine
Giocare contro il computer
Provi ad aprirlo? Dimmi cosa vedi e andiamo avanti insieme! 💙✨
