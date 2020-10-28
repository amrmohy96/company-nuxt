<template>
  <Row>
    <Col style="padding: 10px;" span="24" >
      <Carousel v-model="value1" loop>
        <CarouselItem v-for="slider in sliders" :key="slider.id">
          <div class="demo-carousel">
            <img style="width: 100% ; max-height: 250px;" :src="`${$images(slider.image,'org')}`">
          </div>
        </CarouselItem>
      </Carousel>
    </Col>
  </Row>
</template>

<script>
import Loading from "~/components/Loading";

export default {
  name: "Sliders",
  components: {Loading},
  data() {
    return {
      sliders: [],
      loading: true,
      value1: 0
    }
  },
  created() {
    this.fetchSliders();
    console.log('data')
  },
  methods: {
    fetchSliders() {
      this.loading = true;
      let url = `${process.env.moduleUrl}/sliders`;
      this.$axios.$get(url)
        .then(res => {
          console.log(res)
          this.sliders = res.data;
          this.loading = false;
        }).catch(err => {
        console.log(err)
      })
    }
  }
}
</script>

<style scoped>

</style>
