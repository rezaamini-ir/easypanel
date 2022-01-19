<template>
  <Layout :sidebar="true">
    <div class="content">
      <nav>
        <!-- To use other icons here, you need to import them in the Shortcut component -->
        <h1>EasyPanel</h1>
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
