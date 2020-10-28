<template>
  <div class="container">
    <h3>home</h3>
    <sliders/>
    <Testimonials/>
    <div>
    </div>
  </div>
</template>

<script>
import Sliders from "~/components/home/Sliders";
import Testimonials from "@/components/home/Testimonials";
export default {
  components: {Testimonials, Sliders}
}
</script>

<style>

</style>
