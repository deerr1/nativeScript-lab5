<template>
  <Page>
    <ActionBar>
      <NavigationButton
        @tap="$navigateBack()"
        android.systemIcon="ic_menu_back"
      />
      <Label :text="album.title" wrap="true" />
    </ActionBar>
    <StackLayout>
      <GridLayout rows="auto" columns="*" class="container">
        <Label row="0" :text="user.name" textWrap="true" @tap="userDetail" class="username"/>
      </GridLayout>
      <ListView for="pict in pictures">
        <v-template>
          <GridLayout rows="auto, auto" columns="*">
            <Image row="0" :src="pict.url + '.png'" stretch="none" />
            <Label row="1" :text="pict.title" textWrap="true" />
          </GridLayout>
        </v-template>
      </ListView>
    </StackLayout>
  </Page>
</template>

<script>
import { Http } from "@nativescript/core";
import UserDetail from "@/components/UserDetail.vue";
export default {
  props: ["id"],
  components: {
    UserDetail
  },
  data: function () {
    return {
      album: {
        userId: 1,
        id: 1,
        title: "quidem molestiae enim",
      },
      pictures: [
        {
          albumId: 1,
          id: 1,
          title: "accusamus beatae ad facilis cum similique qui sunt",
          url: "https://via.placeholder.com/600/92c952",
          thumbnailUrl: "https://via.placeholder.com/150/92c952",
        },
      ],
      user: {
        id: 1,
        name: "",
        username: "",
        email: "Sincere@april.biz",
        address: {
          street: "Kulas Light",
          suite: "Apt. 556",
          city: "Gwenborough",
          zipcode: "92998-3874",
          geo: {
            lat: "-37.3159",
            lng: "81.1496",
          },
        },
        phone: "1-770-736-8031 x56442",
        website: "hildegard.org",
        company: {
          name: "Romaguera-Crona",
          catchPhrase: "Multi-layered client-server neural-net",
          bs: "harness real-time e-markets",
        },
      },
    };
  },
  mounted() {
    Http.request({
      url: "http://jsonplaceholder.typicode.com/albums/" + this.id,
      method: "GET",
    }).then((res) => {
      this.album = res.content.toJSON();

      Http.request({
        url:
          "http://jsonplaceholder.typicode.com/photos?albumId=" +
          this.album.id,
        method: "GET",
      }).then((res) => {
        this.pictures = res.content.toJSON();
      });

      Http.request({
        url: "http://jsonplaceholder.typicode.com/users/" + this.album.userId,
        method: "GET",
      }).then((res) => {
        this.user = res.content.toJSON();
      });
    });
  },
  methods: {
    userDetail() {
      this.$navigateTo(UserDetail, { frame: "albums" , props: { id: this.user.id }});
    },
  },
};
</script>

<style>
.container {
  /* width: 100%; */
  margin: 1%, 2%, 0, 2%;
}
.username {
  font-size: 20vw;
  color: orange;
}
</style>
