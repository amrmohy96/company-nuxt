<template>
  <div>
    <h1>{{service.name}}</h1>
    <Loading v-if="loading"/>
    <Row v-else>
      <Col style="padding: 10px" span="24" >

          <div style="text-align:center">
            <img  :src="`${$images(service.image)}`">
          </div>

      </Col>
    </Row>
  </div>
</template>

<script>
import Loading from "~/components/Loading";

export default {
  name: "clients",
  components: {Loading},
  data() {
    return {
      service: {},
      loading: true,
    }
  },
  created() {
    this.fetchClients();
  },
  methods: {
    fetchClients() {
      this.loading = true;
      let url = `${process.env.moduleUrl}/services/${this.$route.params.id}`;
      this.$axios.$get(url)
        .then(res => {
          console.log(res)
          this.service = res;
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
