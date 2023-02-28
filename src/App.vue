<script>
import axios from "axios";
import DetailComponent from "./components/DetailComponent.vue";
import ImageComponent from "./components/ImageComponent.vue";
import UnavailableView from "./components/UnavailableView.vue";

export default{
    data() {
        return {
            women: false,
            men: false,
            neither: false,
            productIndex: 1,
            product: {},
            loading: false,
            oneStar: false,
            twoStar: false,
            threeStar: false,
            fourStar: false,
            fiveStar: false,
        };
    },
    methods: {
        async fetchData() {
            this.loading = true;
            try {
                if (this.productIndex < 20) {
                    ++this.productIndex;
                }
                else {
                    this.productIndex = 1;
                }
                const { data } = await axios({
                    url: `https://fakestoreapi.com/products/${this.productIndex}`,
                    method: "get",
                });
                this.product = data;
                this.loading = false;
                this.changeClass();
                this.displayRating() 
            }
            catch (error) {
                console.log(error);
            }
        },
        changeClass() {
            if (this.product.category === "women's clothing") {
                this.women = true;
                this.men = false;
                this.neither = false;
            }
            else if (this.product.category === "men's clothing") {
                this.men = true;
                this.women = false;
                this.neither = false;
            }
            else {
                this.neither = true;
                this.women = false;
                this.men = false;
            }
        },
        displayRating() {
            this.oneStar = false
            this.twoStar = false
            this.threeStar = false
            this.fourStar = false
            this.fiveStar = false
            if(this.product.rating.rate >= 4.5) {
                this.oneStar = true
                this.twoStar = true
                this.threeStar = true
                this.fourStar = true
                this.fiveStar = true
            } else if(this.product.rating.rate >= 3.5) {
                this.oneStar = true
                this.twoStar = true
                this.threeStar = true
                this.fourStar = true
            } else if(this.product.rating.rate >= 2.5) {
                this.oneStar = true
                this.twoStar = true
                this.threeStar = true
            } else if(this.product.rating.rate >= 1.5) {
                this.oneStar = true
                this.twoStar = true
            } else if(this.product.rating.rate >= 0.5) {
                this.oneStar = true
            }
        }
    },
    created() {
        this.fetchData();
        this.changeClass();
      },
    components: { UnavailableView, DetailComponent, ImageComponent }
}
</script>

<template>
  <div 
    class="container" 
    :class="{bgWomen: women, bgMen: men, bgNeither: neither, bgPattern: men||women}"
  >
    <div 
    class="card" 
    :class="{sadFace: neither}"
    >
      <ImageComponent 
        v-bind="product" 
        :men="men" 
        :women="women" 
        :neither="neither"
      >
      </ImageComponent>
      <DetailComponent 
        v-bind="product" 
        :men="men" 
        :women="women" 
        :neither="neither"
        :oneStar="oneStar" 
        :twoStar="twoStar" 
        :threeStar="threeStar" 
        :fourStar="fourStar" 
        :fiveStar="fiveStar" 
        @fetchData="fetchData"
      >
      </DetailComponent>
      <UnavailableView 
        :neither="neither" 
        @fetchData="fetchData"
      >
      </UnavailableView>
    </div>
  </div>
  <div v-if="loading" id="loader"></div>
</template>

<style scoped>

.container {
  max-height: 65vh;
  display: flex;
  justify-content: center;
  align-items: center;
}
.card {
  margin-top: 36vh;
  width: 80%;
  height: 70vh;
  box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
  border-radius: 10px;
  background-color: var(--white);
}
</style>
