<template>
  <Page>
    <ActionBar title="Information" icon="">
      <NavigationButton
        @tap="$navigateBack()"
        android.systemIcon="ic_menu_back"
      />
    </ActionBar>
    <StackLayout class="container">
      <GridLayout rows="auto, auto, auto, auto" columns="*">
        <GridLayout row="0" rows="auto" columns="*, *">
            <Label text="username:" col="0" textWrap="true" />
            <Label :text="user.username" col="1" textWrap="true" />
        </GridLayout>
        <GridLayout row="1" rows="auto" columns="*, *">
            <Label text="Name:" col="0" textWrap="true" />
            <Label :text="user.name" col="1" textWrap="true" />
        </GridLayout>
        <GridLayout row="2" rows="auto" columns="*, *">
            <Label text="phone:" col="0" textWrap="true" />
            <Label :text="user.phone" col="1" textWrap="true" />
        </GridLayout>
        <GridLayout row="3" rows="auto" columns="*, *">
            <Label text="website:" col="0" textWrap="true" />
            <Label :text="user.website" col="1" textWrap="true" />
        </GridLayout>
      </GridLayout>
    </StackLayout>
  </Page>
</template>

<script>
import { Http } from "@nativescript/core";
export default {
  props: ["id"],
  data: function () {
    return {
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
      url: "http://jsonplaceholder.typicode.com/users/" + this.id,
      method: "GET",
    }).then((res) => {
      this.user = res.content.toJSON();
    });
  },
};
</script>

<style scoped>
.container {
  margin: auto;
  margin: 5%, 3%, 0, 3%;
  font-size: 17vw;
}

</style>
