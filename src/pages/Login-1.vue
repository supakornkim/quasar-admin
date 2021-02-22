<template>
  <q-layout>
    <q-page-container>
      <q-page class="flex bg-image flex-center">
        <q-card v-bind:style="$q.screen.lt.sm?{'width': '80%'}:{'width':'30%'}">
          <q-card-section>
            <q-avatar size="103px" class="absolute-center shadow-10">
              <img src="profile.svg">
            </q-avatar>
          </q-card-section>
          <q-card-section>
            <div class="text-center q-pt-lg">
              <div class="col text-h6 ellipsis">
                Log in
              </div>
            </div>
          </q-card-section>
          <q-card-section>
            <q-form
              class="q-gutter-md"
            >
              <q-input
                filled
                v-model="data.body.username"
                label="Username"
                lazy-rules
              />

              <q-input
                type="password"
                filled
                v-model="data.body.password"
                label="Password"
                lazy-rules

              />

              <div>
                <q-btn label="Login" @click="testfunc()" type="button" color="primary"/>
              </div>
            </q-form>
          </q-card-section>
        </q-card>
      </q-page>
    </q-page-container>
  </q-layout>
</template>

<script>
    export default {
        data() {
            return {
              data : {
                body : {
                  username: 'manager',
                  password: '1234'
                }

              }

            }
        },
        methods: {
          testfunc() {
            console.log(this.data)
            this.$auth.login(this.data)
            .then(response => {
              //this.$router.replace('/')
              //this.$store.commit('auth/setUserData', (data) => { return { user: data.user } })
              this.$axios
                .post('/api/system/connect','')
                .then(result => {
                  console.log(result.data.user)
                  //console.log(this.data, "investdetail")
                  this.$store.commit('auth/setUserData', (result) => { return { id: result.data.user.uid } })
                })
              console.log(response)
              //this.$auth.fetch()
              //this.$store.dispatch('auth/loginCallback')
              //this.store.commit('auth/setUserData', (data) => { return { id: data.id } })
            })
          }
        }
    }
</script>

<style>

  .bg-image {
   background-image: linear-gradient(135deg, #7028e4 0%, #e5b2ca 100%);
  }
</style>
