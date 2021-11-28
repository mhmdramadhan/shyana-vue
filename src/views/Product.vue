<template>
  <div class="product">
    <HeaderShayna />
    <!-- Breadcrumb Section Begin -->
    <div class="breacrumb-section">
      <div class="container">
        <div class="row">
          <div class="col-lg-12">
            <div class="breadcrumb-text product-more text-left">
              <router-link to="/"><i class="fa fa-home"></i> Home</router-link>
              <span>Detail</span>
            </div>
          </div>
        </div>
      </div>
    </div>
    <!-- Breadcrumb Section Begin -->

    <!-- Product Shop Section Begin -->
    <section class="product-shop spad page-details">
      <div class="container">
        <div class="row">
          <div class="col-lg-12">
            <div class="row">
              <div class="col-lg-6">
                <div class="product-pic-zoom">
                  <img class="product-big-img" :src="gambar_default" alt="" />
                </div>
                <div class="product-thumbs">
                  <carousel
                    :dots="false"
                    :nav="false"
                    class="product-thumbs-track ps-slider"
                  >
                    <div
                      class="pt"
                      @click="changeImage(thumbs[0])"
                      :class="thumbs[0] == gambar_default ? 'active' : ''"
                    >
                      <img src="img/mickey1.jpg" alt="" />
                    </div>

                    <div
                      class="pt"
                      @click="changeImage(thumbs[1])"
                      :class="thumbs[1] == gambar_default ? 'active' : ''"
                    >
                      <img src="img/mickey2.jpg" alt="" />
                    </div>

                    <div
                      class="pt"
                      @click="changeImage(thumbs[2])"
                      :class="thumbs[2] == gambar_default ? 'active' : ''"
                    >
                      <img src="img/mickey3.jpg" alt="" />
                    </div>

                    <div
                      class="pt"
                      @click="changeImage(thumbs[3])"
                      :class="thumbs[3] == gambar_default ? 'active' : ''"
                    >
                      <img src="img/mickey4.jpg" alt="" />
                    </div>
                  </carousel>
                </div>
              </div>
              <div class="col-lg-6">
                <div class="product-details text-left">
                  <div class="pd-title">
                    <span>{{ productDetails.type }}</span>
                    <h3>{{ productDetails.name }}</h3>
                  </div>
                  <div class="pd-desc">
                    <div v-html="productDetails.description"></div>
                    <h4>${{ productDetails.price }}</h4>
                  </div>
                  <div class="quantity">
                    <router-link to="/cart" class="primary-btn pd-cart"
                      >Add To Cart</router-link
                    >
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
    <!-- Product Shop Section End -->
    <RelatedproductShayna />
    <FooterShayna />
  </div>
</template>

<script>
import HeaderShayna from "@/components/HeaderShayna";
import FooterShayna from "@/components/FooterShayna";
import RelatedproductShayna from "@/components/RelatedproductShayna";

import carousel from "vue-owl-carousel";

import axios from "axios";

export default {
  name: "product",
  components: { HeaderShayna, FooterShayna, carousel, RelatedproductShayna },
  data() {
    return {
      gambar_default: "",
      thumbs: [
        "img/mickey1.jpg",
        "img/mickey2.jpg",
        "img/mickey3.jpg",
        "img/mickey4.jpg",
      ],
      // mengambil id dari route
      idProduct: this.$route.params.id,

      productDetails: [],
    };
  },
  methods: {
    changeImage(urlImage) {
      this.gambar_default = urlImage;
    },

    setDataPicture(data) {
      // replace object productdetail dengan data dari api
      this.productDetails = data;
      // replace product gambar default dengan data dari api (galleries)
      this.gambar_default = data.galleries[0].photo;
    },
  },
  mounted() {
    axios
      .get("http://127.0.0.1:8001/api/products", {
        params: {
          id: this.idProduct,
        },
      })
      .then((res) => (this.setDataPicture(res.data.data)))
      .catch((err) => console.log(err));
  },
};
</script>


<style>
.product-thumbs .pt {
  margin-right: 10px;
}
</style>