<script setup lang="ts">
import { ref, reactive } from 'vue'
const title = 'Training'
const subtitle = 'Here is where you can learn how to use Vue.js'
const msg = 'AZoom Da Nang Training'
const rawHtml = '<p>Hello <strong>AZoom Team</strong> <em>Da Nang</em></p>'
const id = 'training-id'
const id2 = 'training-id-2'
const id3 = 'training-id-3'
const disabled = true
const dynamicAttrs = {
  id: 'training-id-4',
  class: 'training-class',
  style: 'color: red; font-size: 2rem;'
}

const count = ref(0)
const state = reactive({
  count: 0
})

const increment = () => {
  count.value++
}

const incrementState = () => {
  state.count++
}

const decrement = () => {
  count.value--
}

const decrementState = () => {
  state.count--
}
</script>

<template>
  <div class="training">
    <div class="header">
      <h1>{{ title }}</h1>
      <p>{{ subtitle }}</p>
    </div>

    <div class="group">
      <span class="description">Text Interpolation</span>
      <span>{{ msg }}</span>
    </div>

    <div class="group">
      <span class="description">Raw HTML</span>
      <div v-html="rawHtml"></div>
    </div>

    <div class="group">
      <span class="description">Attribute Bindings</span>
      <div v-bind:id="id2">v-bind:id="id"</div>
      <div :id="id3">:id="id"</div>
      <div :id>:id</div>
      <button :disabled="disabled">Disabled Button</button>
      <div v-bind="dynamicAttrs">Dynamic Attrs</div>
    </div>

    <div class="group">
      <span class="description">ref</span>
      <button @click="increment">Increment</button>
      <button @click="decrement">decrement</button>
      <div>Count: {{ count }}</div>
    </div>

    <div class="group">
      <span class="description">reactive</span>
      <button @click="incrementState">Increment State</button>
      <button @click="decrementState">Decrement State</button>
      <div>Count: {{ state.count }}</div>
    </div>
  </div>
</template>

<style scoped>
.training {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.training > .group {
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #000000;
  border-radius: 0.5rem;
  color: #ffffff;
  font-size: 1.5rem;
  padding: 1rem;
  position: relative;
  flex-direction: column;
  gap: 0.5rem;
}

.training > .group > .description {
  position: absolute;
  top: 10px;
  left: 10px;
  font-size: 13px;
  color: #d9d9d9;
}
</style>
