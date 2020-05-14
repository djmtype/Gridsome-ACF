<template>
	<Layout>
		<h1 v-html="$page.wordPressPost.title" />
		<h2 v-if="$page.wordPressPost.acf.writer"> 
<a href="#writer">{{ $page.wordPressPost.acf.writer.title }}</a>
</h2>


		<img v-if="$page.wordPressPost.featuredMedia" :src="$page.wordPressPost.featuredMedia.sourceUrl" :width="$page.wordPressPost.featuredMedia.mediaDetails.width" :alt="$page.wordPressPost.featuredMedia.altText" />
		<div v-html="$page.wordPressPost.content" />

<template v-if="$page.wordPressPost.acf.writer">
		<div id="writer">
			<h2 v-html="$page.wordPressPost.acf.writer.title" />

			<p v-html="$page.wordPressPost.acf.writer.content" />

			

<div v-for="(item, index) in $page.wordPressPost.acf.writer.acf.socialProfile" :key="index">
		<dl :class="'profile-' + item.name.toLowerCase().trim()">
		<dt>Name:</dt> <dd>{{ item.name }}</dd>
		<dt>ID:</dt> <dd>{{ item.userId }}</dd>
		</dl>
	</div>
				
		</div>
		<!-- /#writer -->
</template>

		<template v-if="$page.wordPressPost.categories.length">
			<h4>Posted in</h4>
			<ul class="list categories">
				<li v-for="category in $page.wordPressPost.categories" :key="category.id">
					<g-link :to="category.path">{{ category.title }}</g-link>
				</li>
			</ul>
		</template>
		<template v-if="$page.wordPressPost.tags.length">
			<h4>Tags</h4>
			<ul class="list tags">
				<li v-for="tag in $page.wordPressPost.tags" :key="tag.id">
					<g-link :to="tag.path">{{ tag.title }}</g-link>
				</li>
			</ul>
		</template>
	</Layout>
</template>

<page-query>
	query WordPressPost ($id: ID!) {
	wordPressPost(id: $id) {
	title
	content
	acf {
          writer {
            id
            title
            content
            acf {
              socialProfile {
                name
                userId
              }
            }
          }
        }
		featuredMedia {
		sourceUrl
		altText
			mediaDetails {
			width
			}
		}
		categories {
		id
		title
		path
		}
		tags {
		id
		title
		path
		}
	}
	}

</page-query>




<script>
	export default {
		metaInfo() {
			return {
				title: this.$page.wordPressPost.title
			};
		}
	};
</script>

<style>
#writer {
	border: 1px solid gold;
	background-color: ivory;
padding: 2rem;
}
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
		content: ",";
		display: inline-block;
	}

	ul.list li:last-child:after {
		content: "";
	}
</style>