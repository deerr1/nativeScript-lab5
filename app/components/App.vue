<template>
  <TabView
    :selectedIndex="selectedIndex"
    @selectedIndexChange="indexChange"
    androidTabsPosition="bottom"
    selectedTabTextColor="orange"
    tabTextColor="black"
    androidSelectedTabHighlightColor="orange"
  >
    <TabViewItem title="Albums" iconSource="~/images/albums.png">
      <Frame id="albums">
        <Albums :key="firstPage" />
      </Frame>
    </TabViewItem>
    <TabViewItem title="Posts" iconSource="~/images/posts.png" class="btn-nav">
      <Frame id="posts">
        <Posts :key="secondPage" />
      </Frame>
    </TabViewItem>
  </TabView>
</template>

<script>
import Albums from "./Albums.vue";
import Posts from "./Posts.vue";
export default {
  data: function () {
    return {
      selectedIndex: 0,
      firstPage: true,
      secondPage: true,
    };
  },
  components: {
    Albums,
    Posts,
  },
  methods: {
    indexChange(args) {
      this.selectedIndex = args.value;
      if (this.selectedIndex == 0) {
        this.firstPage = !this.firstPage;
      } else {
        this.secondPage = !this.secondPage;
      }
    },
  },
};
</script>

<style scoped>
/* .bottom-nav {
  background-color: orangered;
  color: #fdfdfd;
  font-size: 18;
}

.tabstripitem-active {
  background-color: #e2dfde;
}

.tabstripitem-active:active {
  background-color: #343b5e;
}

MDTabContentItem.first-tabcontent {
  background-color: seashell;
  color: olive;
}
MDBottomNavigation MDTabStrip {
  highlight-color: red;
} */

btn-nav {
  font-size: 50px;
}
</style>
