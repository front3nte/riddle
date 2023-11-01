<script setup lang="ts">
import router from '@/router'
import QuizApp from '../components/QuizApp.vue'
import { useLevelStore } from '../stores/quiz'
import { onMounted } from 'vue';

const levelStore = useLevelStore()
if (!levelStore.reached('final-riddle') && !import.meta.env.VITE_SKIP_ALLOWED) {
  router.push('/fantasy-quiz')
}

onMounted(() => {
  document.body.classList.remove(...levelStore.levels, "start");
  document.body.classList.add("final-riddle")
})

</script>

<template>
  <main>
    <QuizApp start-text="Tretet Näher!" level="final-riddle">
      <p>
        Mit dem Wissen und den Erkenntnissen, die ihr während eurer epischen Reise durch das Land
        gesammelt habt, steht ihr nun vor einem monumentalen, von magischem Leuchten durchzogenen
        Portal. Die Legenden sprechen davon, dass dieses Tor den letzten Hinweis zu eurer heiligen
        Mission beherbergt, aber es kann nicht von jedermann geöffnet werden. Nur diejenigen, die
        die Geheimnisse des Landes entschlüsselt haben, können die Macht dieses Portals freisetzen.
      </p>
      <p>
        Vor euch findet ihr einen antiken Steinpfeiler, in den ein seltsames Pult mit mehreren
        Vertiefungen gemeißelt wurde. Jede dieser Vertiefungen scheint genau die Form eines der
        Symbole und Zahlen zu haben, die ihr während eurer Abenteuer entdeckt habt.
      </p>
      <p>
        Flüsternd durch die Luft hallen die Worte einer alten Sage: "Die Antworten, die ihr sucht,
        sind der Schlüssel, den ihr besitzt. Fügt sie zusammen, vereint ihr Wissen und setzt sie in
        die richtige Reihenfolge, um die magische Sequenz zu vervollständigen."
      </p>
      <p>
        Während ihr die gesammelten Symbole und Zahlen in die Vertiefungen des Pults setzt, spürt
        ihr, wie die Energie des Portals reagiert, jedes Mal stärker werdend, wenn ein weiteres
        Stück des Puzzles an seinen Platz gesetzt wird.
      </p>
      <p>
        Sobald alles an seinem Platz ist, sollt ihr die uralten Worte sprechen: "Durch das Wissen
        der Vergangenheit, öffne dich für unsere Mission!" Wenn ihr richtig liegt, wird sich das
        Portal zum Turm des Palastes von Wesoria öffnen und der letzte Hinweis wird euch enthüllt.
        Wenn nicht, muss das Rätsel von Neuem begonnen werden. Seid wachsam, denn eure Mission ist
        fast erfüllt. Es liegt nun an euch, die Antworten zu kombinieren und das Portal zu öffnen.
      </p>
    </QuizApp>
  </main>
</template>
