<template>
  <Page>
    <ActionBar>
      <NavigationButton
        @tap="$navigateBack()"
        android.systemIcon="ic_menu_back"
      />
      <Label :text="postDetail.title" wrap="true" />
    </ActionBar>
    <ScrollView>
      <StackLayout class="container">
        <GridLayout rows="auto, 10, auto" columns="*">
          <GridLayout row="0" rows="auto" columns="2*, 3*">
            <Label
              col="0"
              :text="user.name"
              class="username"
              @tap="userDetail"
            />
          </GridLayout>
          <GridLayout row="2" rows="auto, auto" columns="*">
            <Label
              row="0"
              :text="postDetail.title"
              textWrap="true"
              class="title text"
            />
            <Label
              row="1"
              :text="postDetail.body"
              textWrap="true"
              class="text"
            />
          </GridLayout>
        </GridLayout>
        <Label text="Comments:" class="title" />
        <GridLayout
          v-for="comment in comments"
          :key="comment.id"
          rows="auto, auto, auto"
          columns="*"
          class="comment"
        >
          <Label row="0" :text="comment.email" textWrap="true" class="username"/>
          <Label row="1" :text="comment.name" textWrap="true" />
          <Label row="2" :text="comment.body" textWrap="true" />
        </GridLayout>
      </StackLayout>
    </ScrollView>
  </Page>
</template>

<script>
import { Http } from "@nativescript/core";
import UserDetail from "@/components/UserDetail.vue";
export default {
  props: ["id"],
  components: {
    UserDetail,
  },
  data: function () {
    return {
      postDetail: {
        userId: 1,
        id: 1,
        title: "",
        body: "",
      },
      comments: [
        {
          postId: 1,
          id: 1,
          name: "",
          email: "",
          body: "",
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
      url: "http://jsonplaceholder.typicode.com/posts/" + this.id,
      method: "GET",
    }).then((res) => {
      this.postDetail = res.content.toJSON();

      Http.request({
        url: "http://jsonplaceholder.typicode.com/comments?postId=" + this.id,
        method: "GET",
      }).then((res) => {
        this.comments = res.content.toJSON();
      });

      Http.request({
        url:
          "http://jsonplaceholder.typicode.com/users/" + this.postDetail.userId,
        method: "GET",
      }).then((res) => {
        this.user = res.content.toJSON();
      });
    });
  },
  methods: {
    userDetail() {
      this.$navigateTo(UserDetail, { frame: "posts" , props: { id: this.postDetail.userId }});
    },
  },
};
</script>

<style scoped>
.container {
  /* width: 100%; */
  margin: 1%, 2%, 0, 2%;
}
.scroll {
  height: 100%;
}
.title {
  font-weight: bold;
  font-size: 18vw;
}
.text {
  font-size: 20vw;
}
.username {
  font-size: 20vw;
  color: orange;
}
.comment {
  margin: 0, 0, 15px, 0;
  font-size: 17vw;
  padding: 0, 0, 0, 3%;
  border-width: 5px;
  border-radius: 10;
  border-color: #343B5E;
}
</style>
