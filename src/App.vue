<template>
  <v-app>
    <v-app-bar app color="grey lighten-4" dark>
      <div class="fill-width" align="center">
        <p class="blog-name">Tommy Liu</p>
      </div>

      <v-row justify="space-around" class="mr-2">
        <span class="group d-inline-flex pa-2">
          <v-btn icon href="https://twitter.com/liutommy880108">
            <v-icon color="grey darken-1" class="pa-2">mdi-twitter</v-icon>
          </v-btn>
          <v-btn icon href="https://www.instagram.com/tom__liu/">
            <v-icon color="grey darken-1" class="pa-2">mdi-instagram</v-icon>
          </v-btn>
          <v-btn icon href="https://www.facebook.com/tommy.liu.3192">
            <v-icon color="grey darken-1" class="pa-2">mdi-facebook</v-icon>
          </v-btn>
          <v-btn icon href="https://github.com/kuanchengLiu">
            <v-icon color="grey darken-1" class="pa-2">mdi-github</v-icon>
          </v-btn>
        </span>
      </v-row>
      <v-row justify="space-around" class="mt-n3" v-if="windowWidth > 850">
        <template>
          <v-tabs background-color="grey lighten-4" grow class="d-inline-flex justify-end" tile>
            <v-tab>
              <v-badge color="grey lighten-4" dot class="blog-appbar-col">
                home
              </v-badge>
            </v-tab>

            <v-tab>
              <v-badge color="grey lighten-4" dot class="blog-appbar-col">
                about
              </v-badge>
            </v-tab>
            <v-tab>
              <v-badge color="grey lighten-4" dot class="blog-appbar-col">
                skill
              </v-badge>
            </v-tab>
            <v-tab>
              <v-badge color="grey lighten-4" dot class="blog-appbar-col">
                experence
              </v-badge>
            </v-tab>
            <v-tab>
              <v-badge color="grey lighten-4" dot class="blog-appbar-col">
                PORTFOLIO
              </v-badge>
            </v-tab>
          </v-tabs>
        </template>
      </v-row>
      <v-row justify="space-around" class="mt-n3" v-else>
        <template>
          <div class="text-center" justify="space-end">
            <v-menu open-on-hover bottom offset-y>
              <template v-slot:activator="{ on, attrs }">
                <v-btn outlined color="grey darken-1" v-bind="attrs" v-on="on">
                  <v-icon color="grey darken-1" class="pa-2">mdi-menu</v-icon>
                </v-btn>
              </template>

              <v-list>
                <v-list-item v-for="(index) in menuItem" :key="index">
                  <v-list-item-title>{{ index }}</v-list-item-title>
                </v-list-item>
              </v-list>
            </v-menu>
          </div>
        </template>
      </v-row>
    </v-app-bar>
    <div>
      <v-main>
        <MainBody />
      </v-main>
    </div>

    <div class="pt-1">
      <v-footer dark padless>
        <v-card flat tile class="blue-grey lighten-1 white--text text-center " style="width: 100%;">
          <v-card-text>
            <v-btn v-for="icon in icons" :key="icon" class="mx-4 white--text" icon>
              <v-icon size="24px">
                {{ icon }}
              </v-icon>
            </v-btn>
          </v-card-text>

          <v-card-text class="white--text pt-0">

          </v-card-text>

          <v-divider></v-divider>

          <v-card-text class="white--text">
            {{ new Date().getFullYear() }} — <strong>Tommy</strong>
          </v-card-text>
        </v-card>
      </v-footer>
    </div>
  </v-app>
</template>

<script>
import MainBody from "./components/MainBody.vue";

export default {
  name: "App",

  components: {
    MainBody,
  },

  data: () => ({
    icons: ["mdi-facebook", "mdi-twitter", "mdi-linkedin", "mdi-instagram"],
    windowWidth: window.innerWidth,
    menuItem: ["HOME", "ABOUT", "SKILL", "EXPERENCE", "PORTFOLIO"]
  }),
  watch: {
    windowHeight(newHeight, oldHeight) {
      this.windowWidth = `it changed to ${newHeight} from ${oldHeight}`;
    }
  },

  mounted() {
    this.$nextTick(() => {
      window.addEventListener('resize', this.onResize);
    })
  },

  beforeDestroy() {
    window.removeEventListener('resize', this.onResize);
  },

  methods: {
    onResize() {
      this.windowWidth = window.innerWidth
    }
  }
};
</script>

<style lang="scss" scoped>
@import "./assets/scss/color.scss";
@import "./assets/scss/main.scss";
</style>
