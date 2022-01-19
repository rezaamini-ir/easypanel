<template>
  <Layout>
    <h1>
      {{ $page.doc.title }}
    </h1>
     <div class="markdown" v-html="$page.doc.content" />
  </Layout>
</template>

<page-query>
query Doc ($path: String!) {
  doc: doc (path: $path) {
    title
    path
    date (format: "D. MMMM YYYY")
    timeToRead
    content
  }
}
</page-query>

<script>
export default {
  metaInfo() {
    return {
      title: this.$page.doc.title,
      meta: [
        { key: 'description', name: 'description', content: this.$page.doc.description }
      ]
    }
  }
}
</script>


<style lang="scss" scoped>
/deep/ > p {
  opacity: .8;
  font-size: 1.1rem;
}

/deep/ > h2, /deep/ > h3, /deep/ > h4, /deep/ > h5, /deep/ > h6 {
  padding-top: 100px;
  margin-top: -80px;
}

/deep/ > h2::before, /deep/ > h3::before, /deep/ > h4::before {
  content: "# ";
}

/deep/ > h2 {
  @include respond-above(md) {
    font-size: 2.3rem;
  }
}

/deep/ > h3 {
  @include respond-above(md) {
    font-size: 1.5rem;
  }
}

/deep/ > h4 {
  @include respond-above(md) {
    font-size: 1.1rem;
  }
}

/deep/ > h5, /deep/ > h6 {
  @include respond-above(md) {
    font-size: 0.9rem;
  }
}


/deep/ > p > img {
    max-width: 100%;
  }

.markdown {
  padding-bottom: 50vh;
}
</style>
