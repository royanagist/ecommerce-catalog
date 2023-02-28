<script>
export default {
    props: {
        neither: Boolean,
        men: Boolean,
        women: Boolean,
        image: String,
        title: String,
    },
}
</script>

<template>
    <div v-if="men||women" class="image" :class="{bgNeither: neither}">
        <img 
            :src="this.image" 
            :alt="this.title"
        >
    </div>
</template>

<style scoped>
.card .image {
  float: left;
  width: 35%;
  height: 100%;
  display: flex;
  justify-content: center;
}
.card .image img {
  padding: 50px;
  max-height: 100%;
  max-width: 80%;
  object-fit: contain;
}
</style>