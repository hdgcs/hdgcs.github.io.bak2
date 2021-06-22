<template>
  <v-app>
    <v-app-bar app color="primary" dark clipped-right>
      最新文章
    </v-app-bar>
    <v-navigation-drawer app bottom clipped right>
      <v-container fluid>
        <v-img
          :src="require('./assets/hdgcs-barcode.jpg')"
          contain
        />
      </v-container>
    </v-navigation-drawer>
    <v-main>
      <v-container fluid>
        <v-list two-line>
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
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import Parser from 'rss-parser'
import config from './config'

export default {
  name: 'App',
  data: function() {
    return {
      posts: [],
    }
  },
  mounted: function() {
    const parser = new Parser()
    parser
      .parseURL(config.wechatRssUrl)
      .then(feed => {
        this.posts = feed.items
      })
  },
  filters: {
    localeDate: function(value) {
      return new Date(value).toLocaleDateString()
    },
  },
};
</script>
