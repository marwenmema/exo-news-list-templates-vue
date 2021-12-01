<template>
  <v-app>
    <v-main>
      <div id="image-slider">
        <v-carousel
          height="220"
          show-arrows-on-hover
          cycle
          interval="10000"
          hide-delimiter-background
        >
          <v-carousel-item
            class="carousel-item"
            v-for="(article, i) in articleData"
            :key="i"
            :href="article.link"
            eager
            dark
          >
            <v-img
              class="article-image"
              :src="article.img"
              alt="Author image"
              height="100%"
              eager
              :style="{
                '-webkit-filter': 'brightness(0.63)',
                transition: '0.3s',
              }"
            />
            <v-container
              class="slide-text-container d-flex text-center fill-height body-2"
              align="center"
              justify="center"
              :style="{
                position: 'absolute',
                top: '-10px',
                left: '0',
                right: '0',
              }"
            >
              <v-row
                class="d-flex flex-column"
                align="center"
                justify="center"
                :style="{ margin: '0 30px' }"
              >
                <v-row
                  class="article-title text-h4 font-weight-medium"
                  v-if="portletSettings.showTitle"
                  :style="{
                    display: '-webkit-box',
                    '-webkit-line-clamp': '1',
                    '-webkit-box-orient': 'vertical',
                    overflow: 'hidden',
                    'font-size': '1.7rem!important',
                    'line-height': '3rem',
                    'padding-bottom': '0px',
                  }"
                >
                  {{ article.title }}
                </v-row>
                <v-row
                  class="article-summary text-subtitle-1"
                  v-if="portletSettings.showSummary"
                  :style="{
                    display: '-webkit-box',
                    '-webkit-line-clamp': '2',
                    '-webkit-box-orient': 'vertical',
                    overflow: 'hidden',
                    'font-size': '14px!important',
                    'line-height': '1.2rem',
                  }"
                >
                  {{ article.summary }}
                </v-row>
                <v-row
                  class="article-info d-flex"
                  justify="center"
                  :style="{
                    'font-size': '12px',
                    'margin-top': '22px',
                  }"
                >
                  <div
                    class="author-container"
                    v-if="portletSettings.showAuthor"
                  >
                    <v-avatar size="24">
                      <v-img
                        class="author-image"
                        :src="article.authorImage"
                        alt="Author image"
                      />
                    </v-avatar>
                    <span class="author-name ml-2">{{
                      article.authorName
                    }}</span>
                  </div>
                  <v-icon
                    class="author-space-seperator mx-1"
                    small
                    v-if="
                      portletSettings.showAuthor && portletSettings.showSpace
                    "
                  >
                    mdi-chevron-right
                  </v-icon>
                  <div class="space-container" v-if="portletSettings.showSpace">
                    <v-avatar size="23" rounded>
                      <v-img
                        class="space-image"
                        :src="article.spaceImage"
                        alt="Space icon"
                      />
                    </v-avatar>
                    <span class="space-name ml-2">{{ article.spaceName }}</span>
                  </div>
                  <div
                    class="date-container ml-4"
                    v-if="portletSettings.showDate"
                  >
                    <v-icon class="date-icon" size="15">mdi-clock</v-icon>
                    <span class="date ml-1">{{ article.date }}</span>
                  </div>
                  <div
                    class="reactions-container d-flex ml-4"
                    v-if="portletSettings.showReactions"
                  >
                    <div class="likes-container">
                      <v-icon class="likes-icon" size="14">mdi-thumb-up</v-icon>
                      <span class="likes-count ml-1">{{ article.likes }}</span>
                    </div>
                    <div class="comments-container ml-2">
                      <v-icon class="comments-icon" size="14"
                        >mdi-comment</v-icon
                      >
                      <span class="comments-count ml-1">{{
                        article.comments
                      }}</span>
                    </div>
                    <div class="views-container ml-2">
                      <v-icon class="views-icon" size="16">mdi-eye</v-icon>
                      <span class="views-count ml-1">{{ article.views }}</span>
                    </div>
                  </div>
                </v-row>
              </v-row>
            </v-container>
          </v-carousel-item>
        </v-carousel>
      </div>
    </v-main>
  </v-app>
</template>

<style>
#image-slider .v-carousel__controls__item {
  height: 20px;
  width: 20px;
  margin: 0 2px;
}
#image-slider .v-carousel__controls__item i:before {
  font-size: 10px;
}
#image-slider .v-carousel__controls__item.v-item--active i {
  opacity: 1;
}
#image-slider .slide-text-container {
  text-shadow: 0 0 4px rgb(0 0 0 / 78%);
}
#image-slider .slide-text-container:hover .article-title {
  text-decoration: underline;
  text-decoration-thickness: 2px;
  text-underline-offset: 6px;
  -webkit-transition: 0.5s;
  -o-transition: 0.5s;
  transition: 0.5s;
}
#image-slider .carousel-item:hover .article-image {
  -webkit-transition: 0.3s;
  -o-transition: 0.3s;
  transition: 0.3s;
  -webkit-transform: scale(1.02);
      -ms-transform: scale(1.02);
          transform: scale(1.02);
}
</style>

<script>
export default {
  name: "Image slider",
  data() {
    return {
      portletSettings: {
        maxArticles: 8,
        orderBy: "latestPublished",
        showHeader: false,
        headerText: "",
        showSeeAllBtn: false,
        seeAllBtnLink: "",
        showTitle: true,
        showSummary: true,
        showImage: true,
        showAuthor: true,
        showDate: true,
        showSpace: true,
        showReactions: true,
      },
      articleData: [
        {
          img: "https://picsum.photos/1801/250",
          link: "https://www.exoplatform.com",
          title: "Welcome to your new digital workplace platform",
          summary:
            "The eXo Platform is widely adopted by employees thanks to its simplicity and ease of use.",
          authorName: "Mary Williams",
          authorImage:
            "https://www.rd.com/wp-content/uploads/2017/09/01-shutterstock_476340928-Irina-Bg.jpg",
          spaceName: "Company news",
          spaceImage: "https://shmector.com/_ph/18/412122157.png",
          date: "Feb 17, 2022",
          likes: "12",
          comments: "14",
          views: "54",
        },
        {
          img: "https://picsum.photos/1802/250",
          link: "https://www.exoplatform.com",
          title:
            "Easily create and publish rich news articles to relevant audiences",
          summary:
            "Create, publish and manage rich internal communication content. Highlight your communications on eXo pages through tailored templates.",
          authorName: "Jessica Anderson",
          authorImage:
            "https://katrollings.com.au/wp-content/uploads/2017/02/headshots_tegan_bondi_white_wall-2945.jpg",
          spaceName: "Human resources",
          spaceImage:
            "https://images.creativemarket.com/0.1.0/ps/414215/580/554/m1/fpnw/wm0/1501.m00.i124.n002.s.c10.207438097-customer-support-icon-in-flat-style-.jpg?1427002763&s=9ed94eb32699e4f0a2b6b27853e6fcb1",
          date: "Feb 2, 2022",
          likes: "15",
          comments: "18",
          views: "62",
        },
        {
          img: "https://picsum.photos/1803/250",
          link: "https://www.exoplatform.com",
          title:
            "Curate internal communications and engage your audience through interactions",
          summary:
            "Easily find your champions and super users, measure your employee engagement across the platform, evaluate and adapt your content strategy. Curate content from your employee communities. Interact with your audience with comments, shares and likes.",
          authorName: "Mary Williams",
          authorImage:
            "https://www.rd.com/wp-content/uploads/2017/09/01-shutterstock_476340928-Irina-Bg.jpg",
          spaceName: "Company news",
          spaceImage: "https://shmector.com/_ph/18/412122157.png",
          date: "Jan 24, 2022",
          likes: "24",
          comments: "10",
          views: "73",
        },
        {
          img: "https://picsum.photos/1804/250",
          link: "https://www.exoplatform.com",
          title: "Create value beyond information",
          summary:
            "Foster internal communities of interest, gamify your employee experience, recognize and reward your employees’ contributions.",
          authorName: "Jessica Anderson",
          authorImage:
            "https://katrollings.com.au/wp-content/uploads/2017/02/headshots_tegan_bondi_white_wall-2945.jpg",
          spaceName: "Human resources",
          spaceImage:
            "https://images.creativemarket.com/0.1.0/ps/414215/580/554/m1/fpnw/wm0/1501.m00.i124.n002.s.c10.207438097-customer-support-icon-in-flat-style-.jpg?1427002763&s=9ed94eb32699e4f0a2b6b27853e6fcb1",
          date: "Jan 11, 2022",
          likes: "13",
          comments: "11",
          views: "42",
        },
      ],
    };
  },
};
</script>
