<template>
  <div>
    <h1>{{ title }}</h1>
    <div class="post-meta"><time>{{ params.date }}</time></div>
    <div v-html="bodyHtml"/>
  </div>
</template>

<script>
import { sourceFileArray } from '../../../../content/posts/json/summary.json'

export default {
  validate({ params }) {
    return sourceFileArray.includes(
      `content/posts/${params.date}-${params.slug}.md`
    )
  },
  asyncData({ params }) {
    return Object.assign(
      {},
      require(`~/content/posts/json/${params.date}-${params.slug}.json`),
      { params }
    )
  },
  head() {
    const title = `${this.title} - jmblog.jp`
    const url = `https://jmblog.jp/posts/${this.params.date}/${
      this.params.slug
    }/`
    return {
      title: title,
      meta: [
        { hid: 'og:url', property: 'og:url', content: url },
        { hid: 'og:title', property: 'og:title', content: title }
      ],
      link: [{ rel: 'canonical', href: url }]
    }
  }
}
</script>



<style>
</style>
<style lang="scss" scoped>
.post-meta {
  font-size: 0.8em;
  color: #888;
  margin-top: -1rem;
  margin-bottom: 2.4rem;
  text-align: right;
}
</style>
