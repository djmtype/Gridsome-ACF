<template>
	<Layout>
		<h1 v-html="$page.wordPressWriter.title" />
		<img v-if="$page.wordPressWriter.featuredMedia" :src="$page.wordPressWriter.featuredMedia.sourceUrl" :width="$page.wordPressWriter.featuredMedia.mediaDetails.width" :alt="$page.wordPressWriter.featuredMedia.altText" />
		<div v-html="$page.wordPressWriter.content" />

		<!-- <div v-html="$page.wordPressWriter.acf.socialProfile" /> -->

<div v-for="(item, index) in $page.wordPressWriter.acf.socialProfile" :key="index">
  <h4 :class="'profile-' + item.name.toLowerCase().trim()">
		Name: {{ item.name }}<br>
  ID: {{ item.userId }}</h4>
</div>


	</Layout>
</template>

<page-query>
	query WordPressWriter ($id: ID!) {
	wordPressWriter(id: $id) {
	title
	content
	acf {
		socialProfile {
			name
			userId
		}
	}
	featuredMedia {
		sourceUrl
		altText
		mediaDetails {
			width
		}
	}

	}
	}
</page-query>

<script>
	export default {
		metaInfo() {
			return {
				title: this.$page.wordPressWriter.title
			}
		}
	}
</script>

<style>
	ul.list {
		list-style: none;
		padding: 0;
	}

	ul.list li {
		display: inline-block;
		margin-right: 0.25em;
	}

	ul.list.tags li a {
		padding: 0.25em 0.5em;
		background-color: lightgray;
	}

	ul.list.categories li:after {
		content: ',';
		display: inline-block;
	}

	ul.list li:last-child:after {
		content: '';
	}
</style>