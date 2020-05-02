<template>
  <div>
    <h2 v-html="post.title" />
    <div v-html="post.content" />

    <p v-html="post.acf.socialProfile"/>


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
