<template>
  <div class="home">
    <HeaderShayna />
    <HeroShayna />
    <BannerShayna />
    <InstaShayna />
    <PartnerShayna />
    <FooterShayna />
  </div>
</template>

<script>
import HeaderShayna from "@/components/HeaderShayna";
import HeroShayna from "@/components/HeroShayna";
import BannerShayna from "@/components/BannerShayna";
import InstaShayna from "@/components/InstaShayna";
import PartnerShayna from "@/components/PartnerShayna";
import FooterShayna from "@/components/FooterShayna";
export default {
  name: "Home",
  components: { HeaderShayna, HeroShayna, BannerShayna, InstaShayna, PartnerShayna, FooterShayna },
};
</script>