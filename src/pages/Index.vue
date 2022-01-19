<template>
  <Layout :sidebar="true">
    <div class="content">
      <nav style="flex-direction: column">
        <!-- To use other icons here, you need to import them in the Shortcut component -->
        <h1>EasyPanel</h1>
        <img src="/easypanel.png" alt="">

        <p style="font-size: 1.2rem">An admin panel for Laravel based on Livewire. Also, We can call it "CRUD Maker" 😃</p>

        <h2>Features: </h2>
        <ul>
          <li class="bold">Easy to install 🚀</li>
          <li>Multi Language</li>
          <li>A tons of features for Fields & Inputs</li>
          <li>RTL and LTR style</li>
          <li>Support CKEditor and Persian Font for RTL mode</li>
          <li class="bold">CRUD Maker GUI! 💡</li>
          <li>Everything is customizable</li>
          <li>A beautiful UI/UX with AdminMart template</li>
          <li>UserProviders and Authentication classes are customizable and you can change them</li>
          <li>Real time validation with Livewire 🚦</li>
        </ul>

        <h2 style="margin-top: 1.5rem">Demo: </h2>
        <img src="/demo.png" alt="" style="margin-top: 1rem">
      </nav>
      <div style="display: flex; justify-content: center">
        <GitLink class="git" size="large" />
      </div>
    </div>
  </Layout>
</template>

<static-query>
query {
  metadata {
    siteName
  }
}
</static-query>

<script>
import GitLink from '~/components/GitLink.vue'
import Shortcut from '~/components/Shortcut.vue'
export default {
  components: {
    GitLink,
    Shortcut
  },
  data() {
    return {
      description: 'EasyPanel is a beautiful, customizable and flexible admin panel creator based on Livewire for Laravel.'
    }
  },
  metaInfo() {
    return {
      title: "Laravel EasyPanel",
      meta: [
        { key: 'description', name: 'description', content: 'EasyPanel is a beautiful, customizable and flexible admin panel creator based on Livewire for Laravel.' }
      ]
    }
  }
}
</script>

<style lang="scss" scoped>

.content {
  display: flex;
  flex-direction: column;
}

h1 {
  max-width: 600px;
  @include respond-above(md) {
    max-width: 1000px;
  }
}



h2 {
  font-size: 1.4rem;
  margin: 0;
}

ul > li {
  font-size: 1.2rem;
}

.bold {
  font-weight: 800;
}

nav {
  display: flex;
  justify-content: space-between;
  flex-direction: column;
  @include respond-above(sm) {
    flex-direction: row;
  }
}
.git {
  margin: 3em 0 0;
  align-self: center;
  @include respond-above(md) {
    margin: 5em 0 0;
  }
}
</style>
