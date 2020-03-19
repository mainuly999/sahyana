<template>
    
    <!-- Women Banner Section Begin -->
    <section class="women-banner spad">
        <div class="container-fluid">
            <div class="row">
                <div class="col-lg-12 mt-5" v-if="products.length > 0">
                    <carousel class="product-slider" v-bind:items="3" :dots="false" :nav="false" :autoplay="true">
                        <div class="product-item" v-for="itemProduct in products" v-bind:key="itemProduct.id">
                            <!-- jadi pada products dibawahkan diambil dari json APInya yand data.data.data nah disitu kita akan ambil id pada data ketiga sebagai id di class="product-item", untuk check silahkan chekc link api yang ada pada munted dibawah  -->
                            <div class="pi-pic">
                                <img v-bind:src="itemProduct.galleries[0].photo" alt="" />
                                <ul>
                                    <li class="w-icon active">
                                        <a href="#"><i class="icon_bag_alt"></i></a>
                                    </li>
                                    <!-- kita ingin id khusus agar ketika diklik maka akan menuju ke produk yang dituju -->
                                    <!-- setellah itu atur dirouter -->
                                    <li class="quick-view"><router-link v-bind:to="'/product/'+itemProduct.id">+ Quick View</router-link></li>
                                </ul>
                            </div>
                            <div class="pi-text">
                                <!-- kuranglebih sama dengan penjelasan diatas  -->
                                <div class="catagory-name">{{itemProduct.type}}</div>
                                <a href="#">
                                    <h5>{{itemProduct.name}}</h5>
                                </a>
                                <div class="product-price">
                                    ${{itemProduct.price}}
                                    <span>$35.00</span>
                                </div>
                            </div>
                        </div>

                    </carousel>
                </div>

                <div class="col-lg-12" v-else>
                    <p>Product terbaru belum tersedia</p>
                </div>
            </div>
        </div>
    </section>
    <!-- Women Banner Section End -->
</template>

<script>
import carousel from 'vue-owl-carousel';
// setelah install npm axios maka
import axios from "axios";

export default {
    name:'WomanShayna',
    components:{
        carousel
    },
    data(){
        return{
            products:[]
        }
    },
    // ambil dari API
    mounted(){
        // get(url yang ada pada psotman bagian product)
        axios.get("http://127.0.0.1:8000/api/products")
            // kemudain res itu untnutk mengambi data diatas, nah kenpa 3 datanya karena data pertama itu general seperti meta,data,dll kemudian data kedua adalah spesifik dnegna nama data begipula data ketiga
            .then(res=>(this.products = res.data.data.data))
            .catch(err=>console.log(err));

        
    }
};
</script>

<style scoped>
.product-item{
    margin-right: 25px;
}
</style>