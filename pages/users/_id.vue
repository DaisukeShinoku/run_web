<template>
<div>
  <ErrorCard
  :display="userNotFound"
  title="404 not find"
  message="ユーザーが存在しません。"
  >
  </ErrorCard>
  <v-container v-if="!userNotFound">
    <v-card class="mx-auto mt-5 pa-5" width="1000px">
      <v-row justify="center">
        <v-col cols="2" style="color: #FFD54F;">
          <v-row justify="center" style="margin-top: 48px;">
            <h1>Lv.1</h1>
          </v-row>
          <v-row justify="center">
            <span>current Level</span>
          </v-row>
        </v-col>
        <v-col cols="4">
          <v-row justify="center">
            <v-avatar size="80">
              <img src="~/assets/default_icon.jpeg" />
            </v-avatar>
          </v-row>
          <v-row justify="center">
            <h2>{{ user.name }}</h2>
          </v-row>
        </v-col>
        <v-col cols="2" style="color: #FFD54F;">
          <v-row justify="center" style="margin-top: 48px;">
            <h1>60</h1>
          </v-row>
          <v-row justify="center">
            <span>Total EXP</span>
          </v-row>
        </v-col>
      </v-row>
      <!-- <v-row justify="center">
        <img src="~/assets/goal.jpeg" width="32px" height="32px" />
      </v-row> -->
      <v-row justify="center" align-content="center">
        <v-col cols="1">
        </v-col>
        <v-col cols="7">
          <v-progress-linear height="10px" value="24">
          </v-progress-linear>
        </v-col>
        <v-col cols="1" style="padding-top: 6px; color: #B0BEC5;">
          60/250
        </v-col>
      </v-row>
      <v-row justify="center">
        <Heatmap></Heatmap>
      </v-row>
    </v-card>
  </v-container>
</div>
</template>

<script>
import axios from '@/plugins/axios'
import ErrorCard from '~/components/ErrorCard.vue'
import Heatmap from '~/components/Heatmap.vue'
export default {
  components: {
    ErrorCard,
    Heatmap
  },
  data () {
    return {
      user: {},
      userNotFound: false,
      errorTitle: 'エラー',
      errorMessage: 'エラーが発生しました。'
    }
  },
  mounted () {
    axios
      .get(`/v1/users/${this.$route.params.id}`)
      .then((response) => { this.user = response.data })
      .catch((error) => {
        if (error.response.status === 404) {
          this.userNotFound = true
          this.errorTitle = '404 not find'
          this.errorMessage = 'ユーザーが存在しません。'
        }
        console.error(error)
      })
  }
}
</script>

<style scoped>
h2 {
  margin-top: 12px;
}
div.user-level {
  margin: 0;
  padding: 0;
}
div.user-level h2 {
  margin: 0;
}
</style>