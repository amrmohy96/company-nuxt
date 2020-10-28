<template>
  <div class="layout">
    <Layout>
      <Header>
        <Menu mode="horizontal" theme="dark" active-name="1">
          <div class="layout-logo"></div>
          <div class="layout-nav">
            <MenuItem name="1">
              <nuxt-link to="/">
                <Icon type="ios-navigate"></Icon>
                Home
              </nuxt-link>

            </MenuItem>
            <MenuItem name="2">
              <nuxt-link to="/services">
                <Icon type="ios-keypad"></Icon>
                Services
              </nuxt-link>
            </MenuItem>
            <MenuItem name="3">
              <nuxt-link to="/teams">
                <Icon type="ios-analytics"></Icon>
                Teams
              </nuxt-link>
            </MenuItem>
            <MenuItem name="4">
              <nuxt-link to="/works">
                <Icon type="ios-paper"></Icon>
                Works
              </nuxt-link>
            </MenuItem>

            <MenuItem name="5">
              <nuxt-link to="/clients">
                <Icon type="ios-paper"></Icon>
                Clients
              </nuxt-link>
            </MenuItem>
          </div>
        </Menu>
      </Header>
      <Content :style="{padding: '0 50px',marginTop:'20px'}">
        <Card>
          <div style="min-height: 200px;">
            <Nuxt/>
          </div>
        </Card>
      </Content>
      <Footer class="layout-footer-center">2011-2016 &copy; TalkingData</Footer>
    </Layout>
  </div>
</template>
<script>
export default {}
</script>
<style scoped>
.layout {
  border: 1px solid #d7dde4;
  background: #f5f7f9;
  position: relative;
  border-radius: 4px;
  overflow: hidden;
}

.layout-logo {
  width: 100px;
  height: 30px;
  background: #5b6270;
  border-radius: 3px;
  float: left;
  position: relative;
  top: 15px;
  left: 20px;
}

.layout-nav {
  width: 550px;
  margin: 0 auto;
  margin-right: 20px;
}

.layout-nav a {
  color: white;
}

.layout-footer-center {
  text-align: center;
}
</style>
