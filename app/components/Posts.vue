<template>
  <Page>
    <ActionBar title="Posts"> </ActionBar>

    <ListView for="post in posts" @itemTap="detailPost">
      <v-template>
        <GridLayout rows="40, auto, auto, 10" columns="*">
          <Label
            row="0"
            textTransform="capitalize"
            textAlignment="left"
            col="0"
            :text="post.title"
            class="title"
          />
          <Label row="2" :text="post.body" class="text" />
        </GridLayout>
      </v-template>
    </ListView>
  </Page>
</template>

<script>
import { Http } from "@nativescript/core";
import PostDetail from "@/components/PostDetail.vue";
export default {
  comments: {
    PostDetail,
  },
  data: function () {
    return {
      posts: ["sdsd"],
    };
  },
  mounted() {
    Http.request({
      url: "http://jsonplaceholder.typicode.com/posts",
      method: "GET",
    }).then((res) => {
      this.posts = res.content.toJSON();
    });
  },
  methods: {
    detailPost(event) {
      this.$navigateTo(PostDetail, {
        frame: "posts",
        props: { id: event.item.id },
      });
    },
  },
};
</script>

<style scoped>
.title {
  font-weight: bold;
  font-size: 18vw;
}
.title {
  font-size: 15vw;
}
</style>
