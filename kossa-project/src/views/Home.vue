<template>
  <v-app id="inspire">
    <v-app-bar app color="white" flat>
      <v-container class="py-0 fill-height">
        <img class="header_logo" src="../assets/logo.png" />

        <v-spacer></v-spacer>
        <v-btn text><v-icon>mdi-home</v-icon></v-btn>
        <v-btn text><v-icon>mdi-chat</v-icon></v-btn>
        <v-btn text><v-icon>mdi-bell</v-icon></v-btn>
        <v-btn text><v-icon>mdi-account</v-icon></v-btn>

        <v-responsive max-width="260">
          <v-text-field
            dense
            flat
            hide-details
            rounded
            solo-inverted
            placeholder="검색어를 입력해주세요"
          ></v-text-field>
        </v-responsive>
      </v-container>
    </v-app-bar>

    <v-main class="grey lighten-3">
      <v-container>
        <v-row>
          <v-col cols="2">
            <v-sheet rounded="lg">
              <v-list color="transparent">
                <v-list-item link color="grey lighten-4">
                  <v-list-item-content>
                    <v-list-item-title>
                      전체 글 보기
                    </v-list-item-title>
                  </v-list-item-content>
                </v-list-item>
                <v-list-item link color="grey lighten-4">
                  <v-list-item-content>
                    <v-list-item-title>
                      인기 글 보기
                    </v-list-item-title>
                  </v-list-item-content>
                </v-list-item>

                <v-divider class="my-2"></v-divider>

                <v-list-item v-for="(menu, index) in board" :key="index" link>
                  <v-list-item-content>
                    <v-list-item-title> # {{ menu }} </v-list-item-title>
                  </v-list-item-content>
                </v-list-item>
              </v-list>
            </v-sheet>
          </v-col>

          <v-col>
            <v-sheet
              class="newPost"
              max-width="90vh"
              min-height="10vh"
              rounded="lg"
            >
              <v-icon>mdi-music-accidental-sharp</v-icon>
              <v-select
                class="tag"
                :items="board"
                solo
                dense
                color="none"
                lavel="Tag"
                v-model="new_posts_tag"
              ></v-select>
              <v-btn class="submit" rounded height="30px" @click="createPost"
                >등록</v-btn
              >
              <v-divider class="devider"></v-divider>
              <v-textarea
                class="description"
                label="당신의 고민을 말해주세요"
                prepend-icon="mdi-account-circle-outline"
                height="120px"
                solo
                no-resize
                color="black"
                v-model="new_post"
              />
            </v-sheet>
            <v-sheet
              class="postsBoard"
              max-width="90vh"
              min-height="70vh"
              rounded="lg"
            >
              <!-- 게시글 -->
              <v-sheet>
                sak;djsakl;d
              </v-sheet>
            </v-sheet>
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
export default {
  data: () => ({
    board: ["군생활", "연애", "부조리", "건의사항", "운동", "기타"],
    new_post: "",
    new_posts_tag: ""
  }),
  methods: {
    createPost() {
      // Add a new document in collection "cities"
      this.$firebase
        .firestore()
        .collection("post")
        .add({
          content: this.new_post,
          tag: this.new_posts_tag
        })
        .then(docRef => {
          console.log("Document written with ID: ", docRef.id);
          this.new_post = "";
          this.new_posts_tag = "";
        })
        .catch(function(error) {
          console.error("Error adding document: ", error);
        });
    }
  }
};
</script>
<style scoped>
.header_logo {
  width: 165px;
  height: 55px;
  margin-right: 20px;
}
.newPost {
  height: 220px;
  margin-bottom: 20px;
  padding: 20px 20px 0 20px;
}
.profil_circle {
  position: relative;
  top: -60px;
}
.submit {
  font-weight: bold;
  color: white;
  float: right;
  width: 80px;
  margin-top: 5px;
}
.tag {
  display: inline-block;
  position: relative;
  right: -8px;
  width: 120px;
  font-size: 13px;
}
.description {
  position: relative;
  top: -5px;
  font-size: 14px;
}
.devider {
  position: relative;
  top: -15px;
}
.v-text-field--box .v-input__slot,
.v-text-field--outline .v-input__slot {
  min-height: auto !important;
  display: flex !important;
  align-items: center !important;
}
</style>
