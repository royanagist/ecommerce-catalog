<script>
import ButtonContainer from './ButtonContainer.vue';

export default {
    props: {
        neither: Boolean,
        men: Boolean,
        women: Boolean,
        title: String,
        category: String,
        description: String,
        price: Number,
        rating: Object,
        oneStar: Boolean,
        twoStar: Boolean,
        threeStar: Boolean,
        fourStar: Boolean,
        fiveStar: Boolean,
    },
    components: { ButtonContainer },
    methods: {
        fetchData(){
            this.$emit('fetchData');
        },

    },
}
</script>

<template>
    <div v-if="men||women" class="detail">
        <div class="title">
            <h1 :class="{colorMen: men, colorWomen: women}">{{ title }}</h1>
        </div>
        <div class="sub-title">
            <div class="category">
                <p>{{ category }}</p>
            </div>
            <div class="rating">
                <p>{{ rating.rate }}/5</p>
                <div class="circle" :class="{colorMen: men, colorWomen: women, buttonMen: oneStar&&men, buttonWomen: oneStar&&women}"></div>
                <div class="circle" :class="{colorMen: men, colorWomen: women, buttonMen: twoStar&&men, buttonWomen: twoStar&&women}"></div>
                <div class="circle" :class="{colorMen: men, colorWomen: women, buttonMen: threeStar&&men, buttonWomen: threeStar&&women}"></div>
                <div class="circle" :class="{colorMen: men, colorWomen: women, buttonMen: fourStar&&men, buttonWomen: fourStar&&women}"></div>
                <div class="circle" :class="{colorMen: men, colorWomen: women, buttonMen: fiveStar&&men, buttonWomen: fiveStar&&women}"></div>
            </div>
        </div>
        <hr class="line">
        <div class="desc">
            <p>{{ description }}</p>
        </div>
        <hr class="line">
        <div class="price">
            <p :class="{colorMen: men, colorWomen: women}">${{ price }}</p>
        </div>
        <ButtonContainer :men="men" :women="women" :neither="neither" @fetchData="fetchData"></ButtonContainer>
    </div>
</template>

<style scoped>
.card .detail {
  float: right;
  width: 60%;
  display: flex;
  flex-direction: column;
  margin-right: 50px;
}
.card .detail .title{
  height: 12vh;
  overflow: hidden;
}
.card .detail .title p{
  font-size: 28px;
  font-weight: 600;
}

.card .detail .sub-title {
  display: flex;
  justify-content: space-between;
}
.card .detail .sub-title .rating{
  display: flex;
  justify-content: space-between;
}
.card .detail .sub-title .circle{
  display: flex;
  justify-content: space-between;
  margin: 1px;
  height: 18px;
  width: 18px;
  border-radius: 50%;
  border: 1px solid;
}
.card .detail .sub-title p{
  font-size: 18px;
  font-weight: 400;
  color: var(--text-title);
  margin-top: 0;
  margin-bottom: 0;
  margin-right: 7px;
}
.card .detail .desc {
  height: 33vh;
  overflow: hidden;
}
.card .detail .desc p{
  font-size: 20px;
  font-weight: 400;
  color: var(--text-desc);
}
.card .detail .price {
  margin: 5px 0;
}
.card .detail .price p{
  font-size: 28px;
  font-weight: 600;
  margin: 0;
}
</style>