<template>
  <div class="d-flex flex-column align-items-center">
    <post v-for="p in posts" :key="p.id" :value="p" />
  </div>
</template>

<script>
import Post from './Post'

export default {
  name: 'PostContainer',
  components: {Post},
  props: ['posts'],
}
</script>