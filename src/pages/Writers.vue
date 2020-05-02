<template>
  <Layout>
    <h1>Writers</h1>
    <ul class="post-list">
      <li v-for="{ node } in $page.allWordPressWriter.edges" :key="node.id">
        <Writer :post="node" />
      </li>
    </ul>
    <Pager :info="$page.allWordPressWriter.pageInfo"/>
  </Layout>
</template>

<page-query>
query Writer ($page: Int) {
  allWordPressWriter (page: $page, perPage: 999) @paginate {
    pageInfo {
      totalPages
      currentPage
    }
   edges {
      node {
        id
        title
        content
       path
       acf {
          socialProfile {
            name
            userId
          }
        }

      }
    } 


  }
}
</page-query>






<script>
import { Pager } from 'gridsome'
import Writer from '~/components/Writer.vue'

export default {
  components: {
    Pager,
    Writer
  },
  metaInfo: {
    title: 'Writers'
  }
}
</script>
