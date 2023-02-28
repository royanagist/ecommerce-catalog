<script>
import axios from "axios";

export default{
  data(){
    return{
      Women: false,
      Men: false,
      Neither: false,
      productIndex: 5,
      product: {},
    }
  },
  methods: {
    async fetchData() {
      try {
        if (this.productIndex < 20) {
          ++this.productIndex ;
        } else {
          this.productIndex = 1 ;
        }
        const { data } = await axios({
          url: `https://fakestoreapi.com/products/${this.productIndex}`,
          method: "get",
        });
        this.product = data
        this.changeClass();
        console.log(this.product);
      } catch (error) {
        console.log(error);
      }
    },
    changeClass() {
      if(this.product.category === "women's clothing"){
        this.Women = true;
        this.Men = false;
        this.Neither =false;
      } else if (this.product.category === "men's clothing"){
        this.Men = true;
        this.Women = false;
        this.Neither =false;
      } else {
        this.Neither =true;
        this.Women = false;
        this.Men = false;
      }
    }
  },
  created() {
    this.fetchData();
    this.changeClass();
  }
}
</script>

<template>
  <div class="container" :class="{bgWomen: Women, bgMen: Men, bgNeither: Neither, bgPattern: Men||Women}">
    <div class="card" :class="{sadFace: Neither}">
      <div v-if="Men||Women" class="image" :class="{bgNeither: Neither}">
        <img 
          :src="this.product.image" 
          :alt="this.product.title"
        >
      </div>
      <div v-if="Men||Women" class="detail">
        <div class="title">
          <h1 :class="{colorMen: Men, colorWomen: Women}">{{ product.title }}</h1>
        </div>
        <div class="sub-title">
          <div class="category">
            <p>{{ product.category }}</p>
          </div>
          <div class="rating">
            <p>{{ product.rating.rate }}/5</p>
          </div>
        </div>
        <hr class="line">
        <div class="desc">
          <p>{{ product.description }}</p>
        </div>
        <hr class="line">
        <div class="price">
          <p :class="{colorMen: Men, colorWomen: Women}">${{ product.price }}</p>
        </div>
        <div class="button-container">
          <div class="buy" :class="{colorMen: Men, colorWomen: Women, buttonMen: Men, buttonWomen: Women}">
            <p>Buy now</p> 
          </div>
          <div class="next" @click="fetchData" :class="{colorMen: Men, colorWomen: Women, colorNeither: Neither}">
            <p>Next product</p> 
          </div>
        </div>
      </div>
      <div v-if="Neither" class="unavailable">
        <p>This product is unavailable to show</p>
        <div class="next-unavailable" @click="fetchData" :class="{colorNeither: Neither}">
          <p>Next product</p> 
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>

/* conditional class */
.colorWomen {
  color: var(--pink)
}
.colorMen {
  color: var(--blue);
}
.colorNeither {
  color: var(--text-title);
}
.bgWomen {
  background-color: var(--bg-women);
}
.bgPattern {
  background-image: url(./assets/bg-pattern.svg);
}
.sadFace {
  background-image: url(./assets/sad-face.png);
  background-repeat: no-repeat;
  background-position: 50% 50%;
}
.bgMen {
  background-color: var(--bg-men);
}
.bgNeither {
  background-color: var(--bg-neither);
}
.buttonMen {
  background-color: var(--blue);
}
.buttonWomen {
  background-color: var(--pink);
}
/* ------------------------------------------------------------- */

.container {
  max-height: 70vh;
  display: flex;
  justify-content: center;
  align-items: center;
}
.card {
  margin-top: 28vh;
  /* display: flex;
  justify-content: center;
  align-items: flex-start; */
  width: 80%;
  height: 70vh;
  box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
  border-radius: 10px;
  background-color: var(--white);
}

.line {
  border: 1px solid rgba(0, 0, 0, 0.2);
  width: 100%;
}

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
.card .detail .sub-title p{
  font-size: 18px;
  font-weight: 400;
  color: var(--text-title);
  margin-top: 0;
  margin-bottom: 0;
}
.card .detail .desc {
  height: 35vh;
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

.card .detail .button-container {
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
  width: 50%;
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
