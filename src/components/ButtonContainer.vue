<script>
export default {
    props: {
        neither: Boolean,
        men: Boolean,
        women: Boolean,
    },
    methods: {
        fetchData() {
            this.$emit('fetchData');
        }
    }
}
</script>

<template>
    <div class="button-container">
        <div class="buy" :class="{colorMen: men, colorWomen: women, buttonMen: men, buttonWomen: women}">
            <p>Buy now</p> 
        </div>
        <div class="next" @click="fetchData" :class="{colorMen: men, colorWomen: women, colorNeither: neither}">
            <p>Next product</p> 
        </div>
    </div>
</template>

<style scoped>
.button-container {
  display: flex;
  width: 100%;
  justify-content: space-between;
  margin-top: 10px;
}
.buy {
  display: flex;
  justify-content: center;
  border: 3px solid;
  border-radius: 4px;
  padding: 10px;
  width: 100%;
  margin-right: 20px;
}
.next   {
  display: flex;
  justify-content: center;
  border: 3px solid;
  border-radius: 4px;
  padding: 10px;
  width: 100%;
  margin-left: 20px;
}
.buy p, .next p {
  margin: 0 auto;
  font-size: 20px;
  font-weight: 600;
}

.buy p {
  color: var(--white);
}
.buy:hover, .next:hover {
  cursor: pointer;
}
</style>