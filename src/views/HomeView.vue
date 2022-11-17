<script setup lang="ts">
import TheWelcome from '../components/TheWelcome.vue';
import { ref, watch } from 'vue';
let celsius = ref<string>();
let fahrenheit = ref<string>();
let tips: string = '请输入温度';
watch(celsius, (celsius) => {
  const tempValue = Number(celsius);
  if (tempValue === 0) {
    tips = '请输入温度';
  } else if (tempValue < 100) {
    tips = '水不能沸腾';
  } else if (tempValue >= 100) {
    tips = '水可以沸腾';
  }
});
const toCelsius = (fahrenheit: number) => {
  return (((fahrenheit - 32) * 5) / 9).toFixed(2);
};
const toFahrenheit = (celsius: number) => {
  return ((celsius * 9) / 5 + 32).toFixed(2);
};
const handleTemperatureChange = (e: Event, type: string) => {
  const tempValue = (e.target as HTMLInputElement).value;
  if (tempValue) {
    if (type === 'celsius') {
      celsius.value = tempValue;
      fahrenheit.value = toFahrenheit(Number(tempValue)).toString();
    } else if (type === 'fahrenheit') {
      fahrenheit.value = tempValue;
      celsius.value = toCelsius(Number(tempValue)).toString();
    }
  } else {
    celsius.value = '';
    fahrenheit.value = '';
  }
};
</script>

<template>
  <main>
    <TheWelcome />
    <div>
      <fieldset>
        <legend>请输入温度（单位：摄氏度）：</legend>
        <input
          type="text"
          :value="celsius"
          @input="handleTemperatureChange($event, 'celsius')"
        />
      </fieldset>
      <fieldset>
        <legend>请输入温度（单位：华氏度）：</legend>
        <input
          type="text"
          :value="fahrenheit"
          @input="handleTemperatureChange($event, 'fahrenheit')"
        />
      </fieldset>
      <p>{{ tips }}</p>
    </div>
  </main>
</template>
