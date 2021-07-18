<template>
  <h2 class="title">Links</h2>
  <ul class="links">
    <li v-for="(link, key) in links" :key="key">
      <a :href="link">https://baptiste.tech/{{ key }}</a>
    </li>
  </ul>
</template>

<script>
export default {
  props: ['links'],
}
</script>

<style>
@import url('../assets/css/links.css');
</style>
