<template>
  <div class="avatar">
    <template v-if="auth">
      <v-menu bottom left>
        <v-btn slot="activator" icon>
          <v-avatar size="32px">
            <img :src="user.avatarUrl">
          </v-avatar>
        </v-btn>
        <v-list>
          <v-list-tile href="/api/auth/logout">
            <v-list-tile-title>Logout</v-list-tile-title>
          </v-list-tile>
        </v-list>
      </v-menu>
    </template>
    <template v-else>
      <v-btn
        rounded
        outlined
        href="/api/auth/github"
      >
        Login
      </v-btn>
    </template>
  </div>
</template>

<script>
  import { mapState } from 'vuex'

  export default{
    computed: mapState(['auth','user']),
  }
</script>

<style>
.v-tabs .v-btn {
  text-transform: none;
}
.avatar {
  align-self: center;
}
.v-menu__activator {
  height: 100%;
}
</style>
