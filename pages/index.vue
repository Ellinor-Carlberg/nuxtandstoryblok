<template>
  <section class="posts">
   <PostPreview v-for="post in posts" 
   :key="post.id"  
   :title="post.title" 
   :excerpt="post.previewText" 
   :thumbnailImage="post.thumbnailUrl" :id="post.id"/>
   

  
  </section>
</template>

<script>
import PostPreview from '@/components/Blog/PostPreview'
export default {
  components: {
PostPreview
  },
  asyncData(context){
    return context.app.$storyapi.get('cdn/stories/', {
      version: process.env.NODE_ENV == 'production' ? 'published' : 'draft',
      starts_with: 'blog/'

    }).then( res => {
      console.log(res.data.stories)
      return {
        posts: res.data.stories.map( bp => {
        return {
          id: bp.slug,
          title: bp.content.title,
          previewText: bp.content.summary,
          thumbnailUrl: bp.content.thumbnail
        }
      })
      }
    }) 
  }
/* 
 data() {
   return {
     posts: [{

       title: 'A first snack',
       previewText: 'this will be awesome',
       thumbnailUrl: 'https://images.unsplash.com/photo-1533417177250-227597f5b264?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1500&q=80',
       id: 'first-post'
     },
     {

       title: 'A second snack',
       previewText: 'this will be awesome',
       thumbnailUrl: 'https://images.unsplash.com/photo-1542282811-943ef1a977c3?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1504&q=80',
       id: 'second-post'
     }
     ]
   }
 } */
}
</script>

<style scoped>

.posts {
  padding-top: 2rem;
  display: flex;
  align-items: center;
  justify-content: center;
  /* flex-direction: column; */
  flex-wrap: wrap; 
}
</style>
