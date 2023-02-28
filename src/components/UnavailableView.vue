<script>
export default {
    props: {
        neither: Boolean,
    },
    methods: {
        fetchData() {
            this.$emit('fetchData');
        }
    }
}
</script>

<template>
    <div v-if="neither" class="unavailable">
        <p>This product is unavailable to show</p>
        <div class="next-unavailable" @click="fetchData" :class="{colorNeither: neither}">
            <p>Next product</p> 
        </div>
    </div>
</template>

<style scoped>
.unavailable {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100%;
}
.unavailable p{
  font-size: 20px;
  font-weight: 400;
}

.next-unavailable {
  display: flex;
  justify-content: center;
  border: 3px solid;
  border-radius: 4px;
  padding: 10px;
  width: 30%;
}
.next-unavailable p{
  margin: 0 auto;
  font-size: 20px;
  font-weight: 600;
}

.next-unavailable:hover {
  cursor: pointer;
}
</style>