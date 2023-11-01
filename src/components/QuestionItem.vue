<script setup lang="ts">
import { ref, reactive, onMounted } from 'vue'
import { useLevelStore } from '../stores/quiz'

const emit = defineEmits(['next'])

const props = defineProps({
  level: String,
  question: String,
  answer: String,
  questionCount: Number,
  displayQuest: Number,
  reachedQuest: Number
})

const levelStore = useLevelStore()
const formState = reactive({ hasError: false, success: false })

const input = ref(null)

const reachedNextLevel =
  levelStore.levels.indexOf(levelStore.level) > levelStore.levels.indexOf(props.level)
const reachedLevelAndQuest =
  (levelStore.reached(props.level) && props.reachedQuest > props.displayQuest) || reachedNextLevel

let givenAnswer: String = reachedLevelAndQuest ? props.answer : ''

onMounted(() => {
  input.value.focus()
})

function submit() {
  if (props.answer === givenAnswer || import.meta.env.VITE_SKIP_ALLOWED === 'true') {
    formState.success = true
    setTimeout(
      () => {
        formState.success = false
        emit('next')
      },
      import.meta.env.VITE_SKIP_ALLOWED === 'true' ? 500 : 3000
    )
  } else {
    formState.hasError = true
    setTimeout(() => {
      formState.hasError = false
    }, 1000)
  }
}
</script>

<template>
  <div class="parchment">
    <div class="parchment__inner">
      <p v-if="formState.success === true">
        Richtig! {{ props.level === 'fantasy-quiz' ? '🧙‍♂️' : '🥳' }} Bewahrt die Antwort gut auf...
      </p>
      <form v-else @submit.prevent="submit">
        <h1>
          {{
            props.displayQuest !== undefined
              ? `Raetsel Nummer ${props.displayQuest}`
              : 'Naechstes Raetsel'
          }}
        </h1>
        <p v-html="props.question"></p>
        <input
          :placeholder="levelStore.level === 'fantasy-quiz' ? '' : 'Deine Antwort'"
          ref="input"
          type="text"
          class="answer"
          v-model="givenAnswer"
          :class="{ error: formState.hasError }"
        />
      </form>
    </div>
  </div>
</template>

<style lang="scss">
body.fantasy-quiz .parchment {
  display: flex;
  justify-content: center;
  align-items: center;
  background: url('/pergament.png') no-repeat;
  background-size: 100% 100%;
  max-width: 100%;
  max-height: 100%;
  color: var(--color-background);

  &__inner {
    padding: 100px 220px;
  }

  input {
    background-color: transparent;
    outline: none;
    border-bottom: 2px var(--color-background);
    border-bottom-style: dotted;
    color: var(--color-background);
  }
}

@keyframes shake {
  from {
    transform: translateX(-2px);
  }
  to {
    transform: translateX(2px);
  }
}

input {
  padding: 15px;
  border-radius: 4px;
  border: none;
  outline: 2px solid var(--outline-color);
  font-size: 22px;
  margin-top: 10px;
  color: white;
  background: var(--input-background-color);
  font-family: var(--base-font);
  transition: all 200ms ease-in-out;

  &:focus {
    outline-width: 4px;
    outline-color: var(--outline-focus-color);
  }

  &.error {
    outline-color: red;
    animation: shake 100ms infinite;
  }
}
</style>
