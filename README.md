# Taidealat
Humanistinen ja taideala
Juokseva rivi:
:: StoryInit [script]
<<widget "ticker">>
  <div class="scroll-row"><span class="scroll-content"><<print _args[0]>></span></div>
<</widget>>
PASSAGE:
<<ticker "Myyjä • Asiakaspalvelija • Kassatyöntekijä • Osastovastaava • Tuoteryhmävastaava •">>

. Perusajatus: missä ongelma yleensä on?

Tickerin ulkonäkö harvoin kaatuu CSS:ään.
Yleisin syy siihen, että se muuttuu “laatikkotöhkäksi”:

Twine lisää automaattisesti <p>-tageja ja rivinvaihtoja ympärille.

Teksti tickerin sisällä on kirjoitettu usealle riville → Twine tekee <br>-tageja ⇒ useita tekstirivejä.

Kun pidät HTML-rivin puhtaana ja yhtenä rivinä, CSS hoitaa loput.

2. CSS-mallipohja (voit kierrättää projektista toiseen)

Lisää tämä Story Stylesheetiin (ja käytä vain yhtä versiota .scroll-row / .scroll-content -luokista per projekti):

/* JUOKSEVA RIVI (AMMATTITICKER) – PERUSMALLI */

.scroll-row {
  width: 100%;
  overflow: hidden;
  white-space: nowrap;
  margin: 1.5rem 0;
  padding: 0.6rem 0;
  background: rgba(0, 0, 0, 0.4);    /* vaihda tarvittaessa */
  border-top: 2px solid #ffb347;
  border-bottom: 2px solid #ffb347;
}

.scroll-content {
  display: inline-block;
  white-space: nowrap;
  will-change: transform;
  font-size: 1.05rem;
  font-weight: 600;
  color: var(--accent-1);            /* tai suora väri esim. #fff */
  animation: scroll-left 40s linear infinite;
}

@keyframes scroll-left {
  from { transform: translateX(0); }
  to   { transform: translateX(-100%); }
}


Jos haluat vaalean version (Kaupan alan tyyliä vastaavan), vaihdat vain .scroll-row:n taustan ja rajat:

.scroll-row {
  width: 100%;
  overflow: hidden;
  white-space: nowrap;
  margin: 1.2rem 0;
  padding: 0.3rem 0.6rem;
  background: #fff7e6;
  border-left: 6px solid #e8ab1f;
}

3. HTML-malli: miten ticker lisätään PASSAGEEN

Tämä on tärkein osa.

Käytä aina tällaista yhtä riviä:

<div class="scroll-row"><span class="scroll-content">Myyjä • Asiakaspalvelija • Kassatyöntekijä • Osastovastaava • Tuoteryhmävastaava • Visualisti • Varastotyöntekijä • Logistiikkakoordinaattori • Verkkokaupan asiakaspalvelija • Verkkokauppakoordinaattori • Markkinointiassistentti • Myyntineuvottelija • Myyntipäällikkö • Ostaja • Retail-asiantuntija • Tuoteasiantuntija •</span></div>


Kolme nyrkkisääntöä:

Älä paina Enteriä <span class="scroll-content"> ja </span> väliin.
→ Sisältö pysyy yhdellä rivillä, eikä Twine lisää <br>-tageja.

Laita ticker omalle rivilleen passagessa, näin:

:: Start
<div class="quiz-page">
  <h1>Kaupan ala</h1>
  <hr>

  <p>Johdantoteksti...</p>

  <div class="scroll-row"><span class="scroll-content">...</span></div>

  <p>Seuraava sisältö...</p>
</div>


Tyhjä rivi ennen ja jälkeen auttaa Twinea olemaan kietomatta sitä <p>-tagiin.

Älä kääri tickeriä <<print>>, listojen (<ul>, <ol>) tai muiden block-elementtien sisään, jos et tiedä tarkkaan mitä teet.
