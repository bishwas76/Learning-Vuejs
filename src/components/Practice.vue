<script>
import { nextTick } from 'vue'

export default {
  data() {
    return {
      objectofAttributes: {
        id: 'wrapper-id',
        class: 'wrapper'
      },
      count: 0,
      isButtonDisabled: false,
      seen: false,
    }
  },
  watch: {
      count(value) {
          if(value > 10) {
              this.count = 0
          }
      }
  },
  methods: {
    async counter() {
      this.count++
      console.log(document.getElementById('counter').textContent)
      await nextTick()
      console.log(document.getElementById('counter').textContent)
    },
    disableButton() {
      if (this.isButtonDisabled === true) {
        this.isButtonDisabled = false
      }
      else {
        this.isButtonDisabled = true
      }
    },
  }
}
</script>

<template>
  <header>
    <div v-bind="objectofAttributes">
      <button v-on:click="counter" v-bind:disabled="isButtonDisabled">
        Counter
      </button>
      <button v-on:click="disableButton">disable</button>
      <span id="counter">
       Result: {{ count }}
      </span>
      <br />
      <span v-once>
          First Count value: {{ count }}
      </span>
      <p v-if="seen">This is my counter</p>
    </div>
  </header>
</template>

<style>
</style>