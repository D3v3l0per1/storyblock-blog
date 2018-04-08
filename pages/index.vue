<template>
  <section id="posts">
    <post-preview v-for="post in posts" :key="post.id" :title="post.title" :excerpt="post.previewText" :thumbnailImage="post.thumbnailURL" :id="post.id" />
  </section>
</template>

<script>
import PostPreview from "@/components/Blog/PostPreview"

export default {
  components: {
    PostPreview
  },
  asyncData (context) {
    return context.app.$storyapi.get('cdn/stories', {
      version: 'draft',
      starts_width: 'blog/'
    }).then(res => {
      return {
        posts: res.data.stories.map(bp => {
          return {
            id: bp.slug,
            title: bp.content.title,
            previewText: bp.content.summary,
            thumbnailURL: bp.content.thumbnail
          }
        })
      }
    })
  }
  // data () {
  //   return {
  //     posts: [
  //       { 
  //         title: "A new Beginning",
  //         previewText: "This will be awesome, don't miss it!",
  //         thumbnailURL: "https://cdn.shopify.com/s/files/1/0883/2790/products/StandardTiRando_1_2048x2048.jpg?v=1454709009",
  //         id: "a-new-beginning"
  //       },
  //       { 
  //         title: "A second Beginning",
  //         previewText: "This will be shitty, don't miss it!",
  //         thumbnailURL: "https://cdn.shopify.com/s/files/1/0883/2790/products/StandardTiRando_1_2048x2048.jpg?v=1454709009",
  //         id: "a-second-beginning"
  //       }
  //     ]
  //   }
  // }
}
</script>

<style>
#posts {
  padding-top: 2rem;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

@media (min-width: 35rem) {
  #posts {
    flex-direction: row;
  }
}
</style>
