<template>
  <Page>
    <ActionBar title="Albums"> </ActionBar>
    <ListView for="album in albums" @itemTap="detalAlbums">
      <v-template>
        <GridLayout rows="auto" columns="*">
            <Label :text="album.title" textWrap="true" class="title"/>
        </GridLayout>
      </v-template>
    </ListView>
  </Page>
</template>

<script>
import { Http } from "@nativescript/core";
import AlbumDetail from "@/components/AlbumDetail.vue";
export default {
  components: {
    AlbumDetail,
  },
  data: function () {
    return {
      albums: [
        {
          userId: 1,
          id: 1,
          title: "quidem molestiae enim",
        },
      ],
    };
  },
  mounted() {
    Http.request({
      url: "http://jsonplaceholder.typicode.com/albums",
      method: "GET",
    }).then(res=>{
      this.albums = res.content.toJSON();
    })
  },
  methods: {
    detalAlbums(event) {
      this.$navigateTo(AlbumDetail, {
        frame: "albums",
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
</style>
