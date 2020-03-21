<template>
    <div>
        <!-- Header Section Begin -->
        <header class="header-section">
            <div class="header-top">
                <div class="container">
                    <div class="ht-left">
                        <div class="mail-service">
                            <i class=" fa fa-envelope"></i> hello.shayna@gmail.com
                        </div>
                        <div class="phone-service">
                            <i class=" fa fa-phone"></i> +628 22081996
                        </div>
                    </div>
                </div>
            </div>
            <div class="container">
                <div class="inner-header">
                    <div class="row">
                        <div class="col-lg-2 col-md-2">
                            <div class="logo">
                                <a href="./index.html">
                                    <img src="img/logo_website_shayna.png" alt="" />
                                </a>
                            </div>
                        </div>
                        <div class="col-lg-7 col-md-7"></div>
                        <div class="col-lg-3 text-right col-md-3">
                            <ul class="nav-right">
                                <li class="cart-icon">
                                    Keranjang Belanja &nbsp;
                                    <a href="#">
                                        <i class="icon_bag_alt"></i>
                                        <span>{{keranjangUser.length}}</span>
                                    </a>
                                    <div class="cart-hover">
                                        <div class="select-items">
                                            <table>
                                                <tbody v-if="keranjangUser.length > 0">

                                                    
                                                    <tr v-for="isina in keranjangUser" v-bind:key="isina.id">
                                                        <td class="si-pic">
                                                            <!-- untuk src kita gak usah pakai {} kita tinggal binding saja dengan : or v-bind-->
                                                            <img class="photo-item" v-bind:src="isina.photo" alt="" />
                                                        </td>
                                                        <td class="si-text">
                                                            <div class="product-selected">
                                                                <p>${{isina.price}} x 1</p>
                                                                <h6>{{isina.name}}</h6>
                                                            </div>
                                                        </td>
                                                        <td @click="removeItem(keranjangUser.index)" class="si-close">
                                                            <i class="ti-close"></i>
                                                        </td>
                                                    </tr>
                                                   

                                                </tbody>

                                                <tbody v-else>
                                                    <tr>
                                                        <td>Tidak Ada Isi Dalam Keranjang</td>
                                                    </tr>
                                                </tbody>
                                            </table>
                                        </div>
                                        <div class="select-total">
                                            <span>total:</span>
                                            <h5>${{totalHarga}},00</h5>
                                        </div>
                                        <div class="select-button">
                                            
                                            <a href="#" class="primary-btn view-card"><router-link to="/cart" style="color:#FFF">VIEW CARD</router-link></a>
                                            
                                            <a href="#" class="primary-btn checkout-btn">CHECK OUT</a>
                                        </div>
                                    </div>
                                </li>
                            </ul>
                        </div>
                    </div>
                </div>
            </div>
        </header>
        <!-- Header End -->
    </div>
</template>
<script>
export default {
    name:'HeaderShayna',
    data(){
      return {
          keranjangUser:[]
      }
    },
    methods:{
       removeItem(index){
            this.keranjangUser.splice(index,1);
            const parsed = JSON.stringify(this.keranjangUser);
            localStorage.setItem('keranjangUser', parsed);
       } 
    },
    // jika keranjangUser tersedia dalam local storage maka dia akan memasukan ke data kerangjangUser diatas
    mounted(){
         if(localStorage.getItem('keranjangUser')){
            try{
                this.keranjangUser = JSON.parse(localStorage.getItem('keranjangUser'));
            } catch(e){
                localStorage.removeItem('keranjangUser');
            }
        }
    },
    computed:{
        totalHarga(){
            // reduce itu seperti melooping tetapi selain looping dia juga akan menghitung
            return this.keranjangUser.reduce(function(items,data){
                return items + data.price;
                // data.price itu diambil dari data array keranjangUser 
            },0)
        }
    }
}
</script>

<style scoped>
.photo-item{
    width: 80px;
    height:80px;
}

</style>