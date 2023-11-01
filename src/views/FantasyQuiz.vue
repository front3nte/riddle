<script setup lang="ts">
import router from '@/router'
import QuizApp from '../components/QuizApp.vue'
import { useLevelStore } from '../stores/quiz'
import { onMounted } from 'vue';

const levelStore = useLevelStore()
if (!levelStore.reached('fantasy-quiz') && !import.meta.env.VITE_SKIP_ALLOWED) {
  router.push('/quiz')
}

onMounted(() => {
  document.body.classList.remove(...levelStore.levels, "start");
  document.body.classList.add("fantasy-quiz")
})

const questions = [
  {
    q: 'Während eurer Reise durch das Reich Schlesi, in dem Drachen den Himmel durchziehen und Weise das Wissen der Welt in ihren Spätis hüten, werdet ihr mit einem uralten Zauberspruch konfrontiert, bekannt nur von den klügsten Magiern. Dieser Zauberspruch erlaubte es, einen Schatz gerecht unter den edlen Rittern aufzuteilen, und dabei genau jenes Überbleibsel zu offenbaren, das keiner der Schatzsucher mehr erhalten konnte. Mit welchem Symbol wurde dieser magische Schlüssel von den Gelehrten auf das Pergament der alten Schriften gezeichnet?',
    a: '%'
  },
  {
    q: 'Nachdem ihr das Rätsel des Zauberspruchs gelöst habt, führt euer Weg euch zu den mächtigen Gilden und Zünften des Spreeufers, die ihre Namen als Banner in die Welt hinaus trugen. Der Name eines jeden solchen Ordens begann mit einem Zeichen, einem Buchstaben, der wie ein Talisman ihre Identität und ihren Stolz schützte. Erzählt mir, oh wackere Reisende, welches mystische Zeichen dem Namen des Ordens voransteht, unter dessen Banner ihr dient?',
    a: ']'
  },
  {
    q: 'Nach einer burgermeisterlichen Wegrast tretet ihr fest entschlossen und dem Wind in eurem Haar in diese wundersame Welt ein, bereit, eure Mission zu erfüllen und das Schicksal des Landes zu verändern. Euer Abenteuer hat gerade erst begonnen. Eure Entdeckungen führen euch zu den Alchemisten und Magiern, die das Schicksal der umliegenden Königreiche bestimmten, wo es ein heiliges Zeichen gibt, das die Kraft besitzt, Energien zu vereinen und getrennte Welten zu einem Ganzen zu verbinden.<br /> Dieses Zeichen wurde von den Gelehrten verehrt, da es das Potential besaß, das Wenige in das Viele zu verwandeln. Welches geheimnisvolle Symbol trugen die Weisen auf ihren Roben, um die Kunst des Zusammenführens und des Ergänzens zu symbolisieren?',
    a: '+'
  },
  {
    q: 'Mit dem gesammelten Wissen reist ihr flux entlang der Bauten weiter, an denen Schatten und Licht in einem ewigen Tanz verschmelzen. Zu jener Zeit existierte einst ein Symbol, das Boten und Gelehrte gleichermaßen verehrten. Es war das Zeichen, welches Welten verband, Nachrichten durch die Winde trug und den Absender mit dem Empfänger verknüpfte. In einer Zeit, in der Worte Macht hatten und Gedanken die Realität formten, welches mystische Zeichen erlaubte es den Weisen, Botschaften über Grenzen und Königreiche hinweg zu senden?',
    a: '@'
  },
  {
    q: 'Durch verschlungene Pfade führt euer Abenteuer euch zu einem altertümlichen Scriptorium hinter einer Wegschranke. In der Dämmerung der Zeit, als Legenden geboren wurden, begebt ihr euch auf eine Reise tief in die Erinnerung eurer Seele. Euch umgeben flüsternde Schatten und das leise Rascheln von Pergament. Eine geheimnisvolle Schriftrolle, geschrieben von einem vergessenen Orakel aus einem verborgenen Königreich, zieht deine Aufmerksamkeit auf sich. Sie spricht von einer magischen Matrix, einem Netz, das die Enden der Welt verbindet und in dem jedes Wesen sein eigenes leuchtendes Portal schaffen kann. Die Worte sind komplex, und die Glyphen tanzen vor deinen Augen. Als ihr beschließt, euer eigenes Portal zu dieser magischen Matrix zu erschaffen, bereitet ihr eure Feder vor und betrachtet die Tinte, die aus den Tränen eines Drachen zu stammen scheint. Bevor ihr jedoch das erste Wort schreibt, gibt es ein entscheidendes Zeichen, das den Pfad öffnet. Welches ist dieses Schlüsselsymbol, das das Tor zu dieser neuen Dimension öffnet?',
    a: '<'
  },
  {
    q: 'Eure Reisen lassen euch nicht zur Ruhe kommen, und bei einer mystischen Orangerie macht ihr die Bekanntschaft der Kodexmagier. Ihr stolpert in einer uralten Bibliothek über ein rätselhaftes Grimoire, das von einem Magier aus dem Reich der Schatten verfasst wurde. In diesem Buch werden Codes und Symbole beschrieben, die es ermöglichen, die Essenz von Botschaften und Weissagungen zu bündeln und hervorzuheben, sodass andere Wanderer und Sucher sie leichter finden können. Mitten in einem verzauberten Lied, das die Macht beschreibt, Worte aus den Tiefen der Äther zu ziehen und sie für alle sichtbar zu machen, gibt es ein Schlüsselsymbol, das diese Magie kanalisiert. Welches Zeichen, oft als Tor oder Anker verwendet, beschwört die Macht, Worte und Gedanken aus dem endlosen Fluss der Erzählungen zu heben?',
    a: '#'
  },
  {
    q: 'Nachdem ihr die Geheimnisse der Kodexmagier enträtselt habt, führt euer Weg euch in den Palast Wesoria, wo Drachen majestätisch am Himmel kreisen und Elfenlieder durch die silbernen Gänge hallen. Ein Elf erzählt euch von einer Legende, die nur den mutigsten Abenteurern bekannt ist. Tief in den Kellern des Palastes, bewacht von Goblins und von Fallen durchzogen, liegt ein vergessener Schrein. An dessen Altar, so erzählen  es die Barden, ruht ein Artefakt von unschätzbarem Wert: Das Relikt der  Vereinigung. Es ist kein Edelstein, kein Gold, sondern ein Symbol, das  die Kraft besitzt, zwei Seelen, zwei Schicksale, zwei Geschichten  miteinander zu verknüpfen, als wären sie eins. Viele Magier und Paladine haben ihr Leben riskiert, um dieses Zeichen zu finden, denn es hält den Schlüssel zu einer Magie, die Welten miteinander verschmelzen kann. Abenteurer, welches Zeichen verbirgt sich hinter der Legende und wartet  darauf, von dir entdeckt zu werden?',
    a: '&'
  },
  {
    q: 'Der Aufstieg aus den Kellern ist gekommen. Ihr konntet hier kraft Tanken, aber der Elf schickt euch weiter in die Empfangshallen von Wesoria, wo Worte Macht besitzen und jedes Symbol eine verborgene Kraft birgt, begegnet ihr als renommierte Sprachmeister uralten Legenden und Mythen. Eine dieser Erzählungen, die in den Liedern der Barden widerhallen, berichtet von einem besonderen Zeichen, das den Beginn einer geheimen Gruppe oder eines mächtigen Zaubers markiert. <br/>Dieses Zeichen, so heißt es, ist wie das Tor zu einer verborgenen Kammer, das sich öffnet, um Schätze, Geheimnisse oder magische Formeln zu umhüllen. Es ist der erste Schritt, um in die Tiefen eines Rätsels einzutauchen, ein Einladungszeichen, das die Neugierigen und Wissbegierigen dazu auffordert, weiterzulesen und tiefer zu graben. Dieses Symbol von größter Bedeutung, da es den Anfang einer jeden großen Entdeckung markiert. Welches geheimnisvolle Zeichen dient als Türöffner zu den verborgenen Geheimnissen?',
    a: '('
  },
  {
    q: 'Eure Vorräte neigen sich dem Ende, doch ihr seid euch Gewiss, dass ihr die letzten Aufgaben auf dieser beschwerlichen Reise gemeinsam meistern könnt. Ihr schreitet empor zum ersten Stock des Palastes, wo Worte und Sätze wie Musik durch die Lüfte schweben, sind dir als bewanderter Geschichtenerzähler viele Geheimnisse bekannt. Die Zentauren, die dort leben und jegliche Aparaturen und Techniken fertigen, erzählen euch von einem feinen, schlanken Zeichen, das es ermöglicht, die Stimme eines anderen wiederzugeben, als ob sie deine eigene wäre.<br />Dieses zarte Symbol, sagen die Alten, hält die Macht, Flüstern aus der Vergangenheit festzuhalten und sie in der Gegenwart erklingen zu lassen. Es ist wie eine kleine Brücke zwischen der Welt der Realität und der Welt der Erinnerung, die es den Sprechenden ermöglicht, das Echo einer anderen Seele zu spüren. Dieses Zeichen wird von Dichtern und Schriftstellern gesucht, um die Worte derer wiederzugeben, die nicht mehr unter uns weilen oder die aus der Ferne sprechen. Welches flüchtige Zeichen trägt die Gabe, Stimmen aus der Ferne in die Nähe zu rufen?',
    a: "'"
  },
  {
    q: 'Im zweiten Stock des Palastes Wesoria erinnert ihr euch an eure Tage als Anführer der Zirkel von Vorderendmagiern, wo Ideen Gestalt annehmen und Meister ihr Handwerk verfeinern, bekannt für ihre herausragenden Fähigkeiten. Jeder dieser Zirkel, getrieben von seiner eigenen Vision und durch manche Schlacht getragen, erreichte einen Wendepunkt. Es wurde beschlossen, die Kräfte zu teilen und die Weisheit zu vervielfachen.<br />Wie ein Fluss, der sich teilt und neue Wege bahnt, verwandelten sich diese beiden Zirkel von Vorderendmagiern unter eurer Führung. Sie teilten ihr Wissen und spalteten sich, wodurch neue Funken der Magie im Orden entfacht wurden. Wo einst zwei Zirkel unter eurem Banner standen und das Bild des Ordens prägten, wie viele beeindruckende Zirkel von Vorderendmagiern sind nun durch diese zauberhafte Wandlung entstanden?',
    a: '4'
  },
  {
    q: 'Im dritten Stock des Palastes, wo Zahlen über das Schicksal bestimmen und Mythen und Magie sich verflechten, wandert ihr als Zahlenweiser, stets auf der Suche nach der Essenz der Numerologie. Es gibt eine besondere Zahl, in deren Schatten viele Aberglauben und Legenden gewachsen sind.<br />In den Herzen vieler gilt sie als Botin des Unglücks, gefürchtet und gemieden, als Bringerin von Veränderungen und Umwälzungen. Aber ebenso wird sie in einigen Gegenden als Schlüssel zu alten Geheimnissen und verborgenen Wahrheiten verehrt. Diese Zahl steht zwischen den Welten der Einzelziffern und der Mehrziffern, balancierend auf der Grenze von Licht und Dunkelheit. Welches mysteriöse Numerikum, in Liedern sowohl gefürchtet als auch verehrt, trägt die Dualität des Glücks und des Unglücks in sich?',
    a: '13'
  },
  {
    q: 'Während eures beschwerlichen Aufstiegs in den vierten Stock des Palastes Wesoria, durchquert von mächtigen magischen Schranken, stolpert ihr über einen verborgenen Eingang zu einer uralten Höhle. Eingeprägt über dem steinernen Torbogen findet ihr eine Inschrift in einer fast vergessenen Sprache. Die Legende besagt, dass diese Höhle das Herzstück der Zahlenmagie beherbergt und nur jene, die ihre tiefsten Geheimnisse kennen, dürfen eintreten.<br />Inmitten der Dunkelheit dieser Höhle, beleuchtet nur von der flackernden Fackel in eurer Hand, seht ihr ein großes Portal mit einer einzelnen Inschrift. Sie spricht von einer Zahl, die weder Anfang noch Ende kennt, die den Beginn aller Dinge markiert und dennoch das Fehlen aller Dinge repräsentiert. Es ist die essentielle Zahl, der Ursprung, von dem alles andere abstammt und zu dem alles zurückkehrt. Welche Zahl öffnet das Tor zur tiefsten Kammer dieser geheimnisvollen Höhle?',
    a: '0'
  }
]
</script>

<template>
  <main>
    <QuizApp
      :questions="questions"
      start-text="Gute Reise!"
      level="fantasy-quiz"
      :wait="true"
      waiting-text="Bei Sonnenuntergang reiten wir los..."
    >
      <h1>Super, ihr seid nicht zu stoppen!</h1>
      <p>
        Nachdem ihr nun das WIM durchwühlt und in alten Mattermost-Chats gekramt habt, legen wir nun
        den Schleier der Fantasie über all die Technik und begeben uns ins Reich der Sagen, Rätsel
        und Mythen.
      </p>
      <p>
        In einem Zeitalter, in dem die Welt noch von ungezähmten Magien durchzogen war, beginnt eure
        Reise. Die Morgensonne wirft die ersten goldenen Strahlen über das Land, während ein kühler
        Wind durch die hohen Baumwipfel der uralten Wälder weht. Ein Hauch von Abenteuer liegt in
        der Luft.
      </p>
      <p>
        Ihr werft euch eure schweren Umhänge über, die mit Symbolen und Runen bestickt sind, die von
        euren vergangenen Abenteuern und Schlachten zeugen. Das Leder eurer Stiefel knirscht leise,
        während ihr eure Schritte auf den alten Pfad lenkt, der sich vor euch durch die Landschaft
        schlängelt. Ihr spürt das Gewicht eures Köchers auf dem Rücken, in dem eure sorgfältig
        gefertigten Pfeile ruhen, bereit für jedes drohende Unheil. An eurer Seite schwingt das
        vertraute Gefühl des Schwertgriffs, poliert und scharf, das Zeichen eines wahren
        Abenteurers.
      </p>
      <p>
        Vor euch breitet sich das sagenumwobene Land aus – Wälder, deren Dunkelheit von Geheimnissen
        und Magie durchzogen ist, Täler, in denen sich Flüsse wie silberne Bänder durch die
        Landschaft schlängeln, und Weiten, die von mystischen Kreaturen und unbekannten Gefahren
        bevölkert sind. Doch mit jedem Schritt, den ihr auf dieser Reise macht, fühlt ihr, dass ihr
        nicht alleine seid. Die Alten des Landes, die Geister und die Götter, sie alle beobachten
        euch, bereit, euch auf eurem Weg zu helfen oder euch herauszufordern.
      </p>
      <p>
        Mit einem festen Entschluss in eurem Herzen und dem Wind in eurem Haar tretet ihr in diese
        wundersame Welt ein, bereit, eure Mission zu erfüllen und das Schicksal des Landes zu
        verändern. Euer Abenteuer hat gerade erst begonnen.
      </p>
    </QuizApp>
  </main>
</template>
