<template>
  <div class="home">
    <HeaderShayna />
    <HeroShayna />
    <WomanShayna />
    <InstaShayna />
    <PartnerShayna />
    <FooterShayna />
  </div>
  
</template>

<script>
import HeaderShayna from "@/components/HeaderShayna"
import HeroShayna from "@/components/HeroShayna" 
import WomanShayna from "@/components/WomanShayna" 
import InstaShayna from "@/components/InstaShayna" 
import PartnerShayna from "@/components/PartnerShayna" 
import FooterShayna from "@/components/FooterShayna" 



export default {
  name: 'Home',
  components: {
    HeaderShayna,
    HeroShayna,
    WomanShayna,
    InstaShayna,
    PartnerShayna,
    FooterShayna
  }
}
</script>
