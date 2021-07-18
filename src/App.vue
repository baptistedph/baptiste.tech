<template>
  <ReposContainer v-if="repos">
    <Repo v-for="repo in repos" :key="repo.name" :name="repo.name" />
  </ReposContainer>
  <div class="loading" v-else>Loading...</div>
  <Links v-if="links" :links="links" />
  <div class="loading" v-else>Loading...</div>
  <Footer />
</template>

<script>
import ReposContainer from './components/ReposContainer.vue'
import Repo from './components/Repo.vue'
import Footer from './components/Footer.vue'
import Links from './components/Links.vue'
import { ref } from '@vue/reactivity'

export default {
  components: {
    ReposContainer,
    Repo,
    Footer,
    Links,
  },
  setup() {
    const repos = ref(null)
    const links = ref(null)

    const getRepos = async () => {
      const res = await fetch('https://api.github.com/users/baptistedph/repos')
      repos.value = await res.json()
    }

    const getLinks = async () => {
      const res = await fetch('https://baptiste.tech/redirects.json', {
        mode: 'no-cors',
      })
      links.value = await res.json()
    }

    getRepos()

    getLinks()

    return {
      repos,
      links,
    }
  },
}
</script>

<style>
@import url('./assets/css/global.css');
</style>
