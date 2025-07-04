<template>
  <div class="win-message">
    🎉 Du hast gewonnen! Du hast {{ attempts }} Versuche gebraucht.
    <br>
    <button @click="$emit('restart')">Nochmal spielen</button>
  </div>
</template>

<script>
export default {
  name: 'WinMessage',
  props: {
    attempts: Number
  }
}
</script>