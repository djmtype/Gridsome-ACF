<template>
  <div>
    <h2 v-html="post.title" />
    
    <h3 v-if="post.acf.writer" v-html="'By ' + post.acf.writer.title" />
   <h3 v-else>From the Editor</h3>
    <div v-html="post.excerpt" />
    <g-link :to="post.path">
      Read More
    </g-link>
  </div>
</template>

<script>
export default {
  props: {
    post: {
      type: Object,
      required: true
    }
  }
}
</script>
