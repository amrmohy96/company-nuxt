<template>
  <div>
    <h1>works</h1>
    <Loading v-if="loading"/>
    <Row v-else>
      <Col style="padding: 10px" span="6" v-for="work in works" :key="work.id">
        <Card>
          <div style="text-align:center">
            <nuxt-link style="float: left" :to="`${ work.link }`">{{ work.name }}</nuxt-link>
            <img style="width: 100%" :src="`${$images(work.image)}`">
            <h3 v-html="work.description"></h3>

          </div>
        </Card>
      </Col>
      <Button v-if="total > to" type="primary" :loading="loading" @click="fetchWorks">
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
      works: [],
      loading: false,
      next_page_url: '',
      current_page: '',
      total: '',
      to: ''
    }
  },
  created() {
    this.fetchWorks();
  },
  methods: {
    fetchWorks() {
      this.loading = true;
      let url = `${process.env.moduleUrl}/works`;
      if (this.next_page_url != '' && this.next_page_url != null) {
        url = this.next_page_url;
      }
      this.$axios.$get(url)
        .then(res => {
          console.log(res)
          if (this.works.length > 0) {
            this.works = [...this.works, ...res.data]
          } else {
            this.works = res.data;
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
