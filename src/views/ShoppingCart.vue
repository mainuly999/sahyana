<template>
    <div>
        <HeaderShayna />

        <!-- Breadcrumb Section Begin -->
        <div class="breacrumb-section">
            <div class="container ">
                <div class="row">
                    <div class="col-lg-12 text-left">
                        <div class="breadcrumb-text product-more">
                            <router-link to="/"><i class="fa fa-home"></i> Home</router-link>
                            <span>Shopping Cart</span>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <!-- Breadcrumb Section Begin -->

        <!-- Shopping Cart Section Begin -->
        <section class="shopping-cart spad">
            <div class="container">
                <div class="row">
                    <div class="col-lg-8">
                        <div class="row">
                            <div class="col-lg-12">
                                <div class="cart-table">
                                    <table>
                                        <thead>
                                            <tr>
                                                <th>Image</th>
                                                <th class="p-name text-center">Product Name</th>
                                                <th>Price</th>
                                                <th>Action</th>
                                            </tr>
                                        </thead>
                                        <tbody>
                                            <tr v-for="isina in keranjangUser" v-bind:key="isina.id">
                                                <td class="cart-pic first-row">
                                                    <img class="image-cart" :src="isina.photo" />
                                                </td>
                                                <td class="cart-title first-row text-center">
                                                    <h5>{{isina.name}}</h5>
                                                </td>
                                                <td class="p-price first-row">${{isina.price}}</td>
                                                <td @click="removeItem(keranjangUser.index)" class="si-close"><i class="ti-close">
                                          
                                                </i></td>
                                            </tr>
                                        </tbody>
                                    </table>
                                </div>
                            </div>
                            <div class="col-lg-8 text-left">
                                <h4 class="mb-4">
                                    Informasi Pembeli:
                                </h4>
                                <div class="user-checkout">
                                    <form>
                                        <div class="form-group">
                                            <label for="namaLengkap">Nama lengkap</label>
                                            <input type="text" class="form-control" id="namaLengkap" aria-describedby="namaHelp" placeholder="Masukan Nama">
                                        </div>
                                        <div class="form-group">
                                            <label for="namaLengkap">Email Address</label>
                                            <input type="email" class="form-control" id="emailAddress" aria-describedby="emailHelp" placeholder="Masukan Email">
                                        </div>
                                        <div class="form-group">
                                            <label for="namaLengkap">No. HP</label>
                                            <input type="text" class="form-control" id="noHP" aria-describedby="noHPHelp" placeholder="Masukan No. HP">
                                        </div>
                                        <div class="form-group">
                                            <label for="alamatLengkap">Alamat Lengkap</label>
                                            <textarea class="form-control" id="alamatLengkap" rows="3"></textarea>
                                        </div>
                                    </form>
                                </div>
                            </div>
                        </div>
                    </div>
                    <div class="col-lg-4">
                        <div class="row">
                            <div class="col-lg-12">
                                <div class="proceed-checkout text-left">
                                    <ul>
                                        <li class="subtotal">ID Transaction <span>#SH12000</span></li>
                                        <li class="subtotal mt-3">Subtotal <span>${{totalHarga}}.00</span></li>
                                        <li class="subtotal mt-3">Pajak <span>${{ditambahPajak}}.00(10%)</span></li>
                                        <li class="subtotal mt-3">Total Biaya <span>${{totalBiaya}}.00</span></li>
                                        <li class="subtotal mt-3">Bank Transfer <span>Mandiri</span></li>
                                        <li class="subtotal mt-3">No. Rekening <span>2208 1996 1403</span></li>
                                        <li class="subtotal mt-3">Nama Penerima <span>Shayna</span></li>
                                    </ul>
                                    <router-link to="/success" class="proceed-btn">I ALREADY PAID</router-link>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </section>
        <!-- Shopping Cart Section End -->
        <FooterShayna/>
    </div>
</template>

<script>
import HeaderShayna from "@/components/HeaderShayna";
import FooterShayna from "@/components/FooterShayna" ;

export default {
    name:'ShoppingCart',
    components:{
        HeaderShayna,
        FooterShayna
    },
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
        },
        ditambahPajak(){
            return (this.totalHarga*10/100);
        },
        totalBiaya(){
            return(this.totalHarga + this.ditambahPajak);
        }
    }
}
</script>

<style  scoped>
.image-cart{
    width: 100px;
    height: 100px;
}
</style>