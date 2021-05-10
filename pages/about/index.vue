<template>
  <section class="about-page">
      <h1>{{title}}</h1>
      <p>{{content}}</p>
  </section>
</template>

<script>
export default {
  asyncData(context){
    return context.app.$storyapi.get('cdn/stories/about', {
      version: 'draft',
      /* starts_with: 'about/' */

    }).then( res => {
      console.log(res.data.story)
        return {
          title: res.data.story.content.title,
          content: res.data.story.content.content
      }
    }) 
  }
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