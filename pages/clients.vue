<template>
  <div>
    <h1>our clients</h1>
    <Loading v-if="loading"/>
    <Row v-else>
      <Col style="padding: 10px" span="6" v-for="client in clients" :key="client.id">
        <Card>
          <div style="text-align:center">
            <img style="width: 100%" :src="`${$images(client.logo)}`">
            <h3>A high quality UI Toolkit based on Vue.js</h3>
          </div>
        </Card>
      </Col>
      <Button v-if="total > to" type="primary" :loading="loading" @click="fetchClients">
        <span v-if="!loading">loadMore</span>
        <span v-else>Loading...</span>
      </Button>
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
      clients: [],
      loading: false,
      next_page_url: '',
      current_page: '',
      total: '',
      to: ''
    }
  },
  created() {
    this.fetchClients();
  },
  methods: {
    fetchClients() {
      this.loading = true;
      let url = `${process.env.moduleUrl}/clients`;
      if (this.next_page_url != '' && this.next_page_url != null) {
        url = this.next_page_url;
      }
      this.$axios.$get(url)
        .then(res => {
          console.log(res)
          if (this.clients.length > 0) {
            this.clients = [...this.clients, ...res.data]
          } else {
            this.clients = res.data;
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
