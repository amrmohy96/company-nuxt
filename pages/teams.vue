<template>
  <div>
    <h1>teams</h1>
    <Loading v-if="loading"/>
    <Row v-else>
      <Col style="padding: 10px" span="6" v-for="team in teams" :key="team.id">
        <Card>
          <div style="text-align:center">
            <img style="width: 100%" :src="`${$images(team.image)}`">
            <h3>{{team.job_title}}</h3>
            <div v-if="team.facebook">
            <nuxt-link :to="`${team.facebook}`">
              <Icon type="logo-facebook" />
            </nuxt-link>
            <nuxt-link :to="`${team.linkedin}`">
              <Icon type="logo-linkedin" />
            </nuxt-link>
            </div>
          </div>
        </Card>
      </Col>
      <Button v-if="total > to" type="primary" :loading="loading" @click="fetchTeams">
        <span v-if="!loading">loadMore</span>
        <span v-else>Loading...</span>
      </Button>
    </Row>
  </div>
</template>

<script>
import Loading from "~/components/Loading";

export default {
  name: "teams",
  components: {Loading},
  data() {
    return {
      teams: [],
      loading: false,
      next_page_url: '',
      current_page: '',
      total: '',
      to: ''
    }
  },
  created() {
    this.fetchTeams();
  },
  methods: {
    fetchTeams() {
      this.loading = true;
      let url = `${process.env.moduleUrl}/teams`;
      if (this.next_page_url != '' && this.next_page_url != null) {
        url = this.next_page_url;
      }
      this.$axios.$get(url)
        .then(res => {
          console.log(res)
          if (this.teams.length > 0) {
            this.teams = [...this.teams, ...res.data]
          } else {
            this.teams = res.data;
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
