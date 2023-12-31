<script setup lang="ts">
import QuestionItem from './QuestionItem.vue'
import { useLevelStore } from '../stores/quiz'
import type { PropType } from 'vue'
import { reactive, onMounted } from 'vue'
import router from '../router'
import SunsetAnimation from './SunsetAnimation.vue'

const levelStore = useLevelStore()

interface Question {
  q: string
  a: string
  e?: string
}

const props = defineProps({
  questions: Array as PropType<Question[]>,
  startText: String,
  level: String,
  wait: Boolean,
  waitingText: String,
  fantasy: Boolean,
  heading: String
})

const state = reactive({
  reachedQuest: 0,
  displayQuest: 0,
  isWaiting: props.wait
})

onMounted(() => {
  // Prevent user from skipping levels
  if (!levelStore.reached(props.level)) {
    console.info('Preventing user from skipping levels')
    router.push({ name: levelStore.level })
  }

  // Materialize quest state from storage
  const storedQuest = localStorage.getItem(props.level)
  if (storedQuest) {
    state.reachedQuest = Number.parseInt(storedQuest)
  }
})

router.beforeResolve((guard) => {
  console.log('watched', guard.params.quest)
  if (guard.params.quest === undefined) {
    return
  }

  if (guard.params.quest === '') {
    state.displayQuest = 0
  }

  const urlQuest = Number.parseInt(guard.params.quest as string)

  if (urlQuest < state.reachedQuest) {
    state.displayQuest = urlQuest
    return
  }
})

function nextQuestion() {
  const reachedLastQuestion = props.questions && state.displayQuest >= props.questions?.length

  if (reachedLastQuestion) {
    console.info('reachedLastQuestion')
    if (levelStore.level === props.level) {
      console.info('increment level')
      levelStore.increment()
    } else {
      console.log('navigating to next level')
      router.push({ name: levelStore.getNextLevel(props.level) })
    }
    return
  }

  if (state.reachedQuest === state.displayQuest) {
    console.info('increment quest')
    state.reachedQuest++
    localStorage.setItem(props.level, String(state.reachedQuest))
  }

  state.displayQuest++
  router.push({ name: props.level, params: { quest: state.displayQuest } })
}

function decode(base64String: string) {
  return atob(base64String)
}
</script>

<template>
  <div v-if="state.displayQuest == 0">
    <slot />
    <div v-if="state.isWaiting">
      <SunsetAnimation @exceeded="state.isWaiting = false" />
      <p class="wait-text">{{ props.waitingText }}</p>
    </div>
    <button v-else class="riddle-start-button" @click="nextQuestion()">
      {{ props.startText }}
    </button>
  </div>
  <div v-else>
    <template v-for="(item, index) in props.questions" :key="`questionItem-${index}`">
      <QuestionItem
        :level="props.level"
        v-if="state.displayQuest == index + 1"
        :display-quest="state.displayQuest"
        :question="item.q"
        :answer="decode(item.a)"
        :emoji="item.e"
        :questionCount="props.questions?.length"
        :reachedQuest="state.reachedQuest"
        @next="nextQuestion()"
        :fantasy="props.fantasy"
        :heading="props.heading"
      />
    </template>
  </div>
</template>

<style lang="scss">
.riddle-start-button {
  padding: 15px 20px;
  font-size: 22px;
  background: transparent;
  border: 2px solid var(--outline-color);
  border-radius: 4px;
  color: var(--color-text);
  min-width: 200px;
  float: right;
  transition: all 300ms ease-in-out;
  cursor: pointer;
  display: flex;
  margin: auto;
  align-items: baseline;
  justify-content: center;
  font-family: var(--base-font);

  .final-riddle & {
    float: none;
    margin-top: 1rem;
  }

  &:hover {
    background-color: var(--outline-color);
    color: white;
  }

  &:active {
    color: var(--outline-color);
    background-color: white;
  }
}

.wait-text {
  text-align: center;
  padding-top: 15px;
  font-style: italic;
  font-weight: bold;
  font-size: 32px;
  font-family: 'My Soul', var(--heading-font);
}
</style>
