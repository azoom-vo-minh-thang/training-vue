<script setup lang="ts">
import { ref, reactive, computed } from 'vue'
const title = 'Training'
const subtitle = 'Here is where you can learn how to use Vue.js'
const msg = 'AZoom Da Nang Training'
const rawHtml = '<p>Hello <strong>AZoom Team</strong> <em>Da Nang</em></p>'
const userProvidedHtml = '<img src="x" onerror="alert(\'XSS Attack\')" />'
const id = 'training-id'
const id2 = 'training-id-2'
const id3 = 'training-id-3'
const disabled = true
const dynamicAttrs = {
  id: 'training-id-4',
  class: 'training-class',
  style: 'color: red; font-size: 2rem;'
}
const list = [
  {
    id: 1,
    name: 'John Doe'
  },
  {
    id: 2,
    name: 'Jane Doe'
  },
  {
    id: 3,
    name: 'Alice'
  },
  {
    id: 4,
    name: 'Bob'
  },
  {
    id: 5,
    name: 'Charlie'
  }
]

const obj = {
  1: {
    name: 'John Doe'
  },
  2: {
    name: 'Jane Doe'
  },
  3: {
    name: 'Alice'
  },
  4: {
    name: 'Bob'
  },
  5: {
    name: 'Charlie'
  }
}

const count = ref(0)
const state = reactive({
  count: 0
})
const firstName = ref('John')
const lastName = ref('Doe')

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

const formatDate = (date: Date) => {
  const d = new Date(date)
  const year = d.getFullYear()
  const month = `${d.getMonth() + 1}`.padStart(2, '0')
  const day = `${d.getDate()}`.padStart(2, '0')
  return `${year}-${month}-${day}`
}

const fullName = computed(() => {
  return `${firstName.value} ${lastName.value}`
})

const writableFullName = computed({
  get: () => `${firstName.value} ${lastName.value}`,
  set: (value: string) => {
    const parts = value.split(' ')
    firstName.value = parts[0]
    lastName.value = parts[1]
  }
})
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
      <span class="description">Raw HTML (XSS Attack)</span>
      <!-- <div v-html="userProvidedHtml"></div> -->
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
      <span class="description">Using JavaScript Expressions</span>
      <div>count + 1 -> {{ count + 1 }}</div>
      <div>msg.split('').reverse().join('') -> {{ msg.split('').reverse().join('') }}</div>
      <div :id="`list-${id}`">:id="`list-${id}`</div>
      <time :title="formatDate(new Date())">{{ formatDate(new Date()) }}</time>
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

    <div class="group">
      <span class="description">computed</span>
      <div>
        First Name
        <input v-model="firstName" placeholder="First Name" />
      </div>
      <div>
        Last Name
        <input v-model="lastName" placeholder="Last Name" />
      </div>

      <div>Full Name: {{ fullName }}</div>
    </div>

    <div class="group">
      <span class="description">Writable computed</span>

      <input v-model="writableFullName" placeholder="First Name" />

      <div>writableFullName: {{ writableFullName }}</div>
    </div>

    <div class="group">
      <span class="description">List Rendering (in)</span>

      <ul>
        <li v-for="item in list" :key="item.id">{{ `${item.id} - ${item.name}` }}</li>
      </ul>
    </div>

    <div class="group">
      <span class="description">List Rendering (of)</span>

      <ul>
        <li v-for="item of list" :key="item.id">{{ `${item.id} - ${item.name}` }}</li>
      </ul>
    </div>

    <div class="group">
      <span class="description">List Rendering (OBJ)</span>

      <ul>
        <li v-for="(value, key, index) in obj" :key="index">
          {{ `index ${index} -> ${key} - ${value.name}` }}
        </li>
      </ul>
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
