<template>
  <div>
    <input
      type="number"
      :value="guess"
      placeholder="Dein Tipp"
      min="1"
      max="100"
      @input="$emit('update:guess', $event.target.valueAsNumber)"
      @keyup.enter="emitGuess"
    />
    <button @click="emitGuess">Rate</button>
    <p v-if="message">{{ message }}</p>
  </div>
</template>

<script>
export default {
  name: 'GameInput',
  props: {
    message: String,
    guess: Number
  },
  methods: {
    emitGuess() {
      this.$emit('guess', this.guess)
    }
  }
}
</script>