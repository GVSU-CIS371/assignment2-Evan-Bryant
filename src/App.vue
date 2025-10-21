<template>
  <div>
    <Beverage
      :isIced="currentTemp === 'Cold'"
      :base="selectedBase"
      :creamer="selectedCreamer"
      :syrup="selectedSyrup"
    />

    <ul>
      <li>
        <template v-for="temp in temps" :key="temp">
          <label>
            <input
              type="radio"
              name="temperature"
              :id="`r${temp}`"
              :value="temp"
              v-model="currentTemp"
            />
            {{ temp }}
          </label>
        </template>
      </li>
    </ul>

    <div class="controls">
      <div class="control">
        <label for="base">Base Beverage</label>
        <select id="base" v-model="selectedBase">
          <option v-for="b in bases" :key="b.id" :value="b">{{ b.name }}</option>
        </select>
      </div>
      <div class="control">
        <label for="creamer">Creamer</label>
        <select id="creamer" v-model="selectedCreamer">
          <option v-for="c in creamers" :key="c.id" :value="c">{{ c.name }}</option>
        </select>
      </div>
      <div class="control">
        <label for="syrup">Syrup</label>
        <select id="syrup" v-model="selectedSyrup">
          <option v-for="s in syrups" :key="s.id" :value="s">{{ s.name }}</option>
        </select>
      </div>
    </div>
  </div>
  
</template>

<script setup lang="ts">
import { ref } from "vue";
import Beverage from "./components/Beverage.vue";
import { temps, currentTemp, bases, creamers, syrups } from "./stores/beverage";

const selectedBase = ref(bases.value[2]);
const selectedCreamer = ref(creamers.value[0]);
const selectedSyrup = ref(syrups.value[0]);
</script>

<style lang="scss">
body,
html {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100%;
  background-color: #6e4228;
  background: linear-gradient(to bottom, #6e4228 0%, #956f5a 100%);
}
ul {
  list-style: none;
}
</style>

<style scoped>
.controls {
  display: flex;
  gap: 1rem;
  justify-content: center;
  margin-top: 1rem;
}
.control {
  display: flex;
  flex-direction: column;
  gap: 0.25rem;
  align-items: flex-start;
}
select {
  padding: 0.25rem 0.5rem;
}
</style>
