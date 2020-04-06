<template>
  <v-fab-transition>
    <v-dialog v-model="dialog" max-width="600px">
      <template v-slot:activator>
        <v-btn fixed bottom right fab dark color="primary" @click="dialog = true">
          <v-icon>mdi-pen</v-icon>
        </v-btn>
      </template>
      <v-card>
        <v-card-title>
          <span class="headline">
            Tweet
          </span>
        </v-card-title>
        <v-card-text>
          <v-textarea
            v-model="content"
            label="What's happening?"
            box
            autofocus
            @keyup.enter="tweetEnter"
          />
        </v-card-text>
        <v-card-actions>
          <v-spacer />
          <v-btn
            icon
            flat
            color="red"
            @click="dialog = false"
          >
            <v-icon>mdi-close</v-icon>
          </v-btn>
          <v-btn
            icon
            flat
            color="green"
            @click="tweet"
          >
            <v-icon>mdi-check</v-icon>
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-fab-transition>
</template>

<script>
export default {
  data() {
    return {
      dialog: false,
      content: null
    }
  },
  methods: {
    async tweet() {
      this.dialog = false
      await this.$axios.post('/api/tweets', { content: this.content })
      this.content = null
      this.$emit('tweeted')
    },
    async tweetEnter(event) {
      if (event.ctrlKey) {
        await this.tweet()
      }
    }
  }
}
</script>

<style>
.v-card__title {
  padding: 8px;
}
.v-card__text {
  padding: 8px;
}
.v-card__actions {
  padding: 8px;
}
</style>
