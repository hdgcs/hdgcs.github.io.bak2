<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <v-container>
        最新文章
      </v-container>  
    </v-app-bar>
    <v-main>
      <v-container>
        <div class="d-flex flex-column flex-md-row">
          <div class="flex">
            <v-list two-line>
              <v-skeleton-loader v-if="!posts.length" max-width="800" type="list-item-avatar-two-line@15" />
              <v-list-item v-for="post in posts" :key="post.link" :href="post.link">
                <v-list-item-avatar>
                  <v-icon class="grey lighten-1" dark>
                    mdi-star-minus
                  </v-icon>
                </v-list-item-avatar>
                <v-list-item-content>
                  <v-list-item-title v-text="post.title"></v-list-item-title>
                  <v-list-item-subtitle>{{ post.pubDate | localeDate }}</v-list-item-subtitle>
                </v-list-item-content>
              </v-list-item>
            </v-list>
          </div>
          <v-divider :vertical="$vuetify.breakpoint.mdAndUp" class="my-4 my-md-0 mx-md-4"></v-divider>
          <div class="d-flex justify-center">
            <div>
              <v-img :src="require('./assets/hdgcs-barcode.jpg')" width="300" contain />
              <div class="text-caption text-center">微信扫一扫，关注该公众号</div>
            </div>
          </div>
        </div>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: 'App',
  data: function() {
    return {
      posts: [],
    }
  },
  mounted: function() {
    fetch("/data.json", { method: "GET" })
      .then(response => response.json())
      .then(data => {
        this.posts = data
      })
  },
  filters: {
    localeDate: function(value) {
      return new Date(value).toLocaleDateString()
    },
  },
};
</script>
