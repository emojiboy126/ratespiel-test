<template>
  <div id="app">
    <h1>Ich habe eine Zahl zwischen 1 und 100 ausgesucht.</h1>
    <p>Versuch, die Zahl zu erraten!</p>

    <GameInput
      v-if="!gameOver"
      :message="message"
      :guess="guess"
      @guess="checkGuess"
      @update:guess="guess = $event"
    />
    <WinMessage
      v-else
      :attempts="attempts"
      @restart="startGame"
    />
  </div>
</template>

<script>
import GameInput from './components/GameInput.vue'
import WinMessage from './components/WinMessage.vue'

export default {
  name: 'App',
  components: { GameInput, WinMessage },
  data() {
    return {
      randomNumber: null,
      guess: null,
      attempts: 0,
      gameOver: false,
      message: '',
    }
  },
  created() {
    this.startGame()
  },
  methods: {
    startGame() {
      this.randomNumber = Math.floor(Math.random() * 100) + 1
      this.guess = null
      this.attempts = 0
      this.gameOver = false
      this.message = ''
    },
    checkGuess(guess) {
      if (guess === null || guess === '') {
        this.message = 'Bitte gib eine Zahl ein.'
        return
      }
      if (guess < 1 || guess > 100) {
        this.message = 'Bitte gib eine Zahl zwischen 1 und 100 ein.'
        this.guess = null
        return
      }
      this.attempts++
      if (guess === this.randomNumber) {
        this.gameOver = true
      } else if (guess > this.randomNumber) {
        this.message = 'Tipp: Die Zahl, die du eingegeben hast, ist zu hoch.'
      } else {
        this.message = 'Tipp: Die Zahl, die du eingegeben hast, ist zu niedrig.'
      }
      this.guess = null
    }
  }
}
</script>

<style>
/* Paste ALL your previous <style> here! No changes needed! */
html, body {
  height: 100%;
  margin: 0;
  padding: 0;
}

body {
  min-height: 100vh;
  width: 100vw;
  margin: 0;
  padding: 0;
  background: linear-gradient(120deg, #e0eaff 0%, #f5fcff 100%);
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
}

#app {
  min-width: 340px;
  max-width: 430px;
  min-height: 380px;
  width: 98vw;
  height: 70vh;
  margin: auto;
  padding: 48px 32px 32px 32px;
  background: #fff;
  border-radius: 22px;
  box-shadow: 0 8px 32px 0 rgba(36, 123, 214, 0.15), 0 1.5px 4px rgba(0,0,0,0.07);
  text-align: center;
  display: flex;
  flex-direction: column;
  justify-content: center;
  position: relative;
}

h1 {
  color: #247bd6;
  font-size: 2em;
  margin-bottom: 24px;
  margin-top: 0;
  font-weight: 800;
  letter-spacing: 0.5px;
}

p {
  font-size: 1.15em;
  color: #424242;
  margin: 0 0 24px 0;
}

input[type='number'] {
  padding: 12px 18px;
  font-size: 1.15em;
  border-radius: 10px;
  border: 1.7px solid #b1c9f7;
  outline: none;
  width: 200px;
  transition: border-color 0.2s, box-shadow 0.2s;
  box-shadow: 0 1px 4px rgba(36,123,214,0.03);
  margin-bottom: 24px;
}

input[type='number']:focus {
  border-color: #247bd6;
  box-shadow: 0 0 0 2px #e0eaff;
}

button {
  background: linear-gradient(90deg, #247bd6 80%, #53b6fc 100%);
  color: #fff;
  border: none;
  border-radius: 10px;
  padding: 12px 28px;
  font-size: 1.1em;
  margin-left: 8px;
  font-weight: 700;
  cursor: pointer;
  box-shadow: 0 2px 8px rgba(36,123,214,0.09);
  transition: background 0.2s, transform 0.1s;
  margin-bottom: 10px;
}

button:hover, button:focus {
  background: linear-gradient(90deg, #53b6fc 60%, #247bd6 100%);
  transform: translateY(-2px) scale(1.05);
}

p[v-if="message"] {
  color: #247bd6;
  margin-top: 18px;
  font-weight: 600;
  min-height: 28px;
  transition: color 0.2s;
}

.win-message {
  background: linear-gradient(90deg, #f0f8ff 60%, #caf0f8 100%);
  color: #247bd6;
  padding: 36px 18px 30px 18px;
  border-radius: 18px;
  margin-top: 30px;
  margin-bottom: 20px;
  font-size: 1.55em;
  font-weight: bold;
  box-shadow: 0 2px 18px 0 rgba(36, 123, 214, 0.08);
  position: relative;
  animation: bounce-in 0.6s;
}

@keyframes bounce-in {
  0% { transform: scale(0.85); opacity: 0; }
  70% { transform: scale(1.1); opacity: 1; }
  100% { transform: scale(1); }
}

.win-message::before {
  content: "🎉🎊🎉";
  position: absolute;
  top: -32px;
  left: 0;
  right: 0;
  font-size: 2.2em;
  text-align: center;
  pointer-events: none;
  animation: confetti-drop 1.2s;
}

@keyframes confetti-drop {
  0% { opacity: 0; transform: translateY(-30px);}
  60% { opacity: 1; transform: translateY(10px);}
  100% { opacity: 1; transform: translateY(0);}
}

@media (max-width: 600px) {
  #app {
    min-width: 98vw;
    max-width: 99vw;
    padding: 28px 4vw;
    height: 90vh;
  }
  input[type='number'] {
    width: 80vw;
    min-width: 120px;
  }
}
</style>