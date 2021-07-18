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
      const res = await fetch('http://localhost:3000/_redirects')
      links.value = filterLinks(await res.text())
    }

    const filterLinks = links => {
      const split = links.split(' ')

      const redirects = {}

      for (let i = 0; i < split.length - 2; i += 2) {
        redirects[split[i].replace(/(\r\n|\n|\r)/gm, '').replace('/', '')] =
          split[i + 1]
      }

      return redirects
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
