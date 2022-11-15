<script setup lang="ts">
import TheWelcome from '../components/TheWelcome.vue';
const handleChange = () => {};
</script>

<template>
  <main>
    <TheWelcome />
    <div>
      <fieldset>
        <legend>请输入温度（单位：ccc）：</legend>
        <input type="text" value="123" :onChange="handleChange" />
      </fieldset>
    </div>
  </main>
</template>
