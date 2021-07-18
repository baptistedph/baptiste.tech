<template>
  <a :href="`https://github.com/baptistedph/${name}`" class="repo"
    ><img
      :src="`https://github-readme-stats.vercel.app/api/pin/?username=baptistedph&repo=${name}`"
      :alt="name"
  /></a>
</template>

<script>
export default {
  props: ['name'],
}
</script>

<style>
@import url('../assets/css/repo.css');
</style>
