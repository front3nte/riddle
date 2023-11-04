<script setup lang="ts">
import router from '@/router'
import QuizApp from '../components/QuizApp.vue'
import { useLevelStore } from '../stores/quiz'
import AnimatedBalloons from '../components/AnimatedBalloons.vue'
import { onMounted } from 'vue'

const levelStore = useLevelStore()
if (!levelStore.reached('quiz') && !(import.meta.env.VITE_SKIP_ALLOWED === 'true')) {
  router.push('/')
}

onMounted(() => {
  document.body.classList.remove(...levelStore.levels)
  document.body.classList.add('quiz', 'start')
})

const questions = [
  {
    q: 'Was ist die erste Ziffer von Jasmins Durchwahl?',
    a: 'OA==',
    e: '📞'
  },
  {
    q: 'Wann hat Antonio auf seiner Tastatur einen echten Bug 🐞 gefunden (dd.mm.yyyy)?',
    a: 'MTUuMTIuMjAyMQ==',
    e: '🐞'
  },
  {
    q: 'Wann hat Daniel davon berichtet, dass eine Theme-Erstellerin Hühner, Feuer und Lamas in die IDE zaubert (dd.mm.yyyy)?',
    a: 'MzAuMDYuMjAyMQ==',
    e: '🐔'
  },
  {
    q: 'Was ist der zweite **Begriff** in der zweiten &lt;h3&gt; in den Notizen vom Frontend Circle vom `${Dritte Antwort}`?',
    a: 'VGFzayBSdW5uZXI=',
    e: '💨'
  },
  {
    q: 'Wer steht auf Nummer `${Erste Antwort}` der Teilnehmer:innen des Frontend Circles vom `${Zweite Antwort}`?',
    a: 'TmFkaW5lIFB1c2No',
    e: '⭕'
  },
  {
    q: 'Wer hat einen Blog Post darüber geschrieben, dass ein bestimmter `${Vierte Antwort}` bei Installation fehlschlägt?',
    a: 'QW5kcukgUGV0cmFrb3c=',
    e: '❌'
  },
  {
    q: 'Welches Unicode-Zeichen ist in der UTF-8-codierung binär mit `01011110` codiert?',
    a: 'Xg==',
    e: '🗡️'
  },
  {
    q: 'Erster Buchstabe des zweiten Wortes von `${Vierte Antwort}`',
    a: 'Ug==',
    e: '🦄'
  },
  {
    q: 'Erster Buchstabe des zweiten Wortes von `${Sechste Antwort}`',
    a: 'UA==',
    e: '🧙🏼‍♂️'
  },
  {
    q: 'const a = `${Dritte Antwort}`;<br> console.log(`${a.vorvorletztesZeichen}${a.vorletzteZeichen}`);<br><br> Was wird hier in der Konsole ausgegeben?',
    a: 'MDI=',
    e: '🐉'
  },
  {
    q: 'Dritter Buchstabe von `${Fünfte Antwort}`',
    a: 'ZA==',
    e: '🕶'
  },
  {
    q: 'Zweiter Buchstabe des zweiten Wortes von `${Fünfte Antwort}`',
    a: 'dQ==',
    e: '🧝'
  }
]
</script>

<template>
  <main>
    <QuizApp :questions="questions" start-text="Los geht's!" level="quiz">
      <h1>Herzlichen Glückwunsch!</h1>
      <p>
        Wir hoffen ihr hattet mächtigen Puzzle-Spaß. Euer Ehrgeiz und eure Sorgfalt hat euch hier
        her geführt. Nun habt ihr tapfer gewartet bis diese Pforte sich öffnet. Doch bevor ihr
        endgültig am Ziel eurer Reise angekommen seid, warten noch ein paar Aufgaben auf euch, die
        es zu lösen gilt. Also nehmt einander an die Hand und macht euch auf die Suche nach der
        verborgenen Botschaft und durchquert das Rätseldickicht...
      </p>
      <p class="wait-text">
        Doch bedenkt: die Weisheiten, die ihr auf dieser Reise sammeln werdet, werden noch von
        Belang sein, also bewahret sie sicher.
      </p>
      <AnimatedBalloons />
    </QuizApp>
  </main>
</template>
