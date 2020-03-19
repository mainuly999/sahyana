<template>
  <div class="product">
    <HeaderShayna />
        <!-- Breadcrumb Section Begin -->
    <div class="breacrumb-section">
        <div class="container text-left">
            <div class="row">
                <div class="col-lg-12">
                    <div class="breadcrumb-text product-more">
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
                                <img class="product-big-img" v-bind:src="gambar_default" alt="" />
                            </div>
                            <div class="product-thumbs" v-if="productDetails.galleries.length > 0">
                                <carousel class="product-thumbs-track ps-slider" :dots="false" :nav="false">
                                    <!-- <div class="pt " v-for="gambar in thumbs" :key="gambar" :data-imgbigurl="gambar" @click="changeImage(gambar)">
                                        <img :src="gambar" alt="" v-bind:class="gambar == gambar_default && thumb ? 'active' : ''" />
                                    </div> -->
                                    <div v-for="ss in productDetails.galleries " v-bind:key="ss.id" class="pt" @click="changeImage(ss.photo)" v-bind:class="ss.photo == gambar_default ? 'active': ''">
                                        <img v-bind:src="ss.photo" alt="" />
                                    </div>
                                </carousel>
                            </div>
                        </div>
                        <div class="col-lg-6">
                            <div class="product-details text-left">
                                <div class="pd-title">
                                    <span>{{productDetails.type}}</span>
                                    <h3>{{productDetails.name}}</h3>
                                </div>
                                <div class="pd-desc">
                                    <p v-html="productDetails.description">
                                     
                                    </p>
                                    <h4>${{productDetails.price}}</h4>
                                </div>
                                <div class="quantity">
                                    <!-- <router-link to="/cart" class="primary-btn pd-cart"> -->
                                    <a @click="saveKeranjang(productDetails.id)" href="#" class="primary-btn pd-cart"> Add To Cart </a> 
                                    <!-- </router-link> -->
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>
    <!-- Product Shop Section End -->

    <RelatedProducts/>
    <FooterShayna />
  </div>
  
</template>

<script>
import HeaderShayna from "@/components/HeaderShayna";
import FooterShayna from "@/components/FooterShayna" ;
import RelatedProducts from "@/components/RelatedProducts" ;
import axios from "axios";

import carousel from "vue-owl-carousel";


export default {
  name: 'Product',
  components: {
    HeaderShayna,
    FooterShayna,
    RelatedProducts,
    carousel
  },
  data(){
      return {
          gambar_default:'',
          productDetails:[],
          keranjangUser:[]
      }
  },
 
  methods:{
      changeImage(urlImage){
          this.gambar_default = urlImage;
        // eslint-disable-next-line no-console
        console.log(this.idProduct);
      },
      setDataPicture(data){
        //   replace object productDetails diatas dengan data dari API
        this.productDetails = data;
        // replace value gambar default dengan dari API (galleries)
        this.gambar_default = data.galleries[0].photo;
      },
      saveKeranjang(idProduct){
        this.keranjangUser.push(idProduct);
        const parsed = JSON.stringify(this.keranjangUser);
        localStorage.setItem('keranjangUser', parsed);
      }
  },
  mounted(){
        if(localStorage.getItem('keranjangUser')){
            try{
                this.keranjangUser = JSON.parse(localStorage.getItem('keranjangUser'));
            } catch(e){
                localStorage.removeItem('keranjangUser');
            }
        }
        axios.get("http://127.0.0.1:8000/api/products/",{
            params:{
                id:this.$route.params.id
            }
        })
        // duaji datanya karena sudah mi diklik quick view artinya sudah masuk satu data 
            .then(res=>(this.setDataPicture(res.data.data)))
            .catch(err=>console.log(err));    
    }
};
</script>

<style scoped>
.product-thumbs .pt{
    margin-right: 15px;
}
</style>