<template>
  <div>
    <div class="columns is-mobile has-text-centered">
      <div class="column is-6">
        <figure class="image is-3by2">
          <img src="../assets/logo.png">
        </figure>
      </div>
      <div class="column is-6">

        <figure class="image is-3by2">
          <img src="../assets/logo.png">
        </figure>
      </div>
    </div>
    <h1 class="title">VueJs Line LIFF Showcase</h1>
    <div class="columns is-mobile">
      <div class="column is-12 has-text-centered buttons">
        <button @click="openWindow()" class="button is-primary">Open Window</button>
        <button @click="closeWindow()" class="button is-info">Close Window</button>
        <button @click="sendMessage()" class="button is-success">Send Message</button>
        <button @click="getProfile()" class="button is-danger">Get Profile</button>
      </div>
    </div>
    <h2 class="subtitle">Profile</h2>
      <div class="columns is-mobile">
        <div class="column is-half is-offset-one-quarter">
          <div class="field is-horizontal">
            <div class="field-label is-normal">
              <label class="label">User ID:</label>
            </div>
            <div class="field-body">
              <div class="field is-narrow">
                <div class="control">
                  {{ profile.userId || '-' }}
                </div>
              </div>
            </div>
          </div>

          <div class="field is-horizontal">
            <div class="field-label is-normal">
              <label class="label">Display Name:</label>
            </div>
            <div class="field-body">
              <div class="field is-narrow">
                <div class="control">
                  {{ profile.displayName || '-' }}
                </div>
              </div>
            </div>
          </div>

          <div class="field is-horizontal">
            <div class="field-label is-normal">
              <label class="label">Picture URL:</label>
            </div>
            <div class="field-body">
              <div class="field is-narrow">
                <div class="control">
                  {{ profile.pictureUrl || '-' }}
                </div>
              </div>
            </div>
          </div>

          <div class="field is-horizontal">
            <div class="field-label is-normal">
              <label class="label">Status Message:</label>
            </div>
            <div class="field-body">
              <div class="field is-narrow">
                <div class="control">
                  {{ profile.statusMessage || '-' }}
                </div>
              </div>
            </div>
          </div>

        </div>
      </div>
    <br>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data: () => ({
    profile: {
      userId: '',
      displayName: '',
      pictureUrl: '',
      statusMessage: ''
    }
  }),
  methods: {
    openWindow () {
      this.$liff.openWindow({
        url: 'https://developers.line.me/en/docs/liff/overview/'
      })
    },
    closeWindow () {
      this.$liff.closeWindow()
    },
    sendMessage () {
      this.$liff.sendMessages([
        {
          type: 'text',
          text: 'You/\'ve successfully sent a message! Hooray!'
        },
        {
          type: 'sticker',
          packageId: '2',
          stickerId: '144'
        }
      ]).then(function () {
        window.alert('Message sent')
      }).catch(function (error) {
        window.alert('Error sending message: ' + error)
      })
    },
    getProfile () {
      let _this = this
      this.$liff.getProfile().then(function (profile) {
        _this.profile = profile
      }).catch(function (error) {
        alert('Error getting profile: ' + error)
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
