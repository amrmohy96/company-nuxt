<template>
  <div>
    <h1>our services</h1>
    <Loading v-if="loading"/>
    <Row v-else>
      <Col style="padding: 10px" span="6" v-for="service in services" :key="service.id">
        <Card>
          <div style="text-align:center">
            <img style="width: 100%" :src="`${$images(service.image)}`">
            <h3>{{service.name}}</h3>
          </div>
        </Card>
      </Col>
      <Button v-if="total > to" type="primary" :loading="loading" @click="fetchServices">
        <span v-if="!loading">loadMore</span>
        <span v-else>Loading...</span>
      </Button>
    </Row>
  </div>
</template>

<script>
import Loading from "~/components/Loading";

export default {
  name: "services",
  components: {Loading},
  data() {
    return {
      services: [],
      loading: false,
      next_page_url: '',
      current_page: '',
      total: '',
      to: ''
    }
  },
  created() {
    this.fetchServices();
  },
  methods: {
    fetchServices() {
      this.loading = true;
      let url = `${process.env.moduleUrl}/services`;
      if (this.next_page_url != '' && this.next_page_url != null) {
        url = this.next_page_url;
      }
      this.$axios.$get(url)
        .then(res => {
          console.log(res)
          if (this.services.length > 0) {
            this.services = [...this.services, ...res.data]
          } else {
            this.services = res.data;
          }

          this.current_page = res.current_page;
          this.next_page_url = res.next_page_url;
          this.to = res.to;
          this.total = res.total;
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
