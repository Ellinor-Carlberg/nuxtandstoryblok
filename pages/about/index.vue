<template>
  <section class="about-page" v-editable="blok">
      <h1>{{title}}</h1>
      <p>{{content}}</p>
  </section>
</template>

<script>
export default {
  asyncData(context){
    return context.app.$storyapi.get('cdn/stories/about', {
     version: process.env.NODE_ENV == 'production' ? 'published' : 'draft'
      /* starts_with: 'about/' */

    }).then( res => {
      console.log(res.data.story)
        return {
           blok: res.data.story.content,
          title: res.data.story.content.title,
          content: res.data.story.content.content
      }
    }) 
  }/* , mounted() {
    this.$storyblok.init()
     this.$storyblok.on('change', ()=> { location.reload(true)})
} */
}
</script>

<style scoped>

.about-page {
  width: 80%;
  max-width: 30rem;
  margin: auto;
}

.about-page p {
  white-space: pre-line;
}

</style>