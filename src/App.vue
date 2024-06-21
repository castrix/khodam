<script setup lang="ts">
import { ref } from 'vue'
import HelloWorld from './components/HelloWorld.vue'
import Particles from './components/Particles.vue'
import listKhodam from './listKhodam.ts'

const colors = ["#ff0000"
  , "#00FFFF"
  , "#AC94F4"
  , "#FFFF00"
]

const KHODAM_STORAGE_KEY = "KHODAM_STORAGE"
const LINKS_STORAGE_KEY = "NODE_STORAGE"

const DEFAULT_EMPTY = "KOSONG"

const inputName = ref("")
const khodam = ref("-")
const linksColor = ref("#ffffff")


const getRandomFromList = (list: Array<string | undefined>, key: string) => {
  const storage = localStorage.getItem(key) || "{}"
  let cache: Record<string, string> = {}
  try {
    cache = JSON.parse(storage)
  } catch { }
  const cacheResult = cache[inputName.value]
  if (cacheResult !== undefined) return cacheResult
  const randomIndex = Math.floor(Math.random() * list.length);
  const filteredList = key === LINKS_STORAGE_KEY ? list.filter(item => item !== linksColor.value) : list
  const result =filteredList[randomIndex]
  cache = { ...cache, [inputName.value]: result || "" }
  localStorage.setItem(key, JSON.stringify(cache))
  return result
}

const handleEnter = (e: any) => {
  e.preventDefault()
  if (!inputName.value) return
  const result = getRandomFromList(listKhodam, KHODAM_STORAGE_KEY) || DEFAULT_EMPTY
  khodam.value = result
  if (result === DEFAULT_EMPTY) {
  linksColor.value = "#ffffff"
  return
  }
  linksColor.value = getRandomFromList(colors, LINKS_STORAGE_KEY) || "#AC94F4"
}

</script>

<template>
  <Particles :key="linksColor" :links="linksColor" />
  <div>
    <a href="https://www.instagram.com/ihsanfr0/" target="_blank"><img src="./assets/rajasiluman.webp" class="logo" alt="Vite logo" /></a>
  </div>
  <div class="content">
    <HelloWorld msg="CEK KHODAM" />
    <form @submit="handleEnter">
      <input v-model="inputName" style="font-size: 25px; padding-left: 5px;" placeholder="nama anda" />
      <button type="submit">>CEK<</button>
    </form>
    <div style="margin-top: 20px;"><code>
    <b>KHODAM:</b>
  </code></div>
    <h1 style="margin-top: 0;">{{ khodam }}</h1>

  </div>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}

.content {
  background-color: rgba(0, 0, 0, 0.8);
  filter: drop-shadow(0 0 4em #646cffaa);
  padding: 5px 30px;
  border-radius: 10px;
}

.logo {
  filter: drop-shadow(0 0 2em #646cffaa);
}

.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
