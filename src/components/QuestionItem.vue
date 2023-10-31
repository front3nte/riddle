<script setup lang="ts">
import { ref, reactive } from 'vue'
import { useLevelStore } from '../stores/quiz'

const emit = defineEmits(['next', 'reset'])

const props = defineProps({
  question: String,
  answer: String,
  questionCount: Number,
  index: Number
})

const levelStore = useLevelStore()
const formState = reactive({ hasError: false, success: false })

const input = ref(null)

let givenAnswer: String

function submit() {
  if (props.answer === givenAnswer || import.meta.env.VITE_SKIP_ALLOWED === 'true') {
    formState.success = true
    setTimeout(
      () => {
        formState.success = false
        emit('next')
        if (props.questionCount && props.index && props.index >= props.questionCount) {
          emit('reset')
          levelStore.increment()
        }
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
      Richtig! {{ levelStore.level === 'fantasy-quiz' ? '🧙‍♂️' : '🥳' }} Bewahrt die Antwort gut
      auf...
    </p>
    <form v-else @submit.prevent="submit">
      <h1>{{ props.index ? `Raetsel Nummer ${props.index + 1}` : 'Naechstes Raetsel' }}</h1>
      <p v-html="props.question"></p>
      <input
        placeholder="Deine Antwort"
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
  background: url('/public/pergament.png') no-repeat;
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
