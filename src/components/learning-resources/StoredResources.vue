<template>
  <ul>
    <learning-resource
      v-for='res in resources'
      :id='res.id'
      :key='res.id'
      :description='res.description'
      :link='res.link'
      :title='res.title'
    >

    </learning-resource>

  </ul>
</template>

<script>
import LearningResource from '@/components/learning-resources/LearningResource';

export default {
  components: { LearningResource },
  inject: ['resources']
};
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
  margin: auto;
  max-width: 40rem;
}
</style>
