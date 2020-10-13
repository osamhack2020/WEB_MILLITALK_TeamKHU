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
              class="createPost"
              max-width="90vh"
              min-height="15vh"
              rounded="lg"
            >
              <div>
                <v-select
                  class="tag"
                  :items="board"
                  prepend-icon="mdi-music-accidental-sharp"
                  dense
                  label="태그"
                ></v-select>
              </div>
              <div>
                <v-icon class="profil_circle"
                  >mdi-account-circle-outline</v-icon
                >
                <textarea
                  class="description"
                  placeholder="고민을 말해주세요"
                ></textarea>
                <v-btn class="submit" rounded>등록</v-btn>
              </div>
            </v-sheet>
            <v-sheet
              class="postsBoard"
              max-width="90vh"
              min-height="70vh"
              rounded="lg"
            >
              <!--  -->
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
    board: ["군생활", "연애", "부조리", "건의사항", "운동", "기타"]
  })
};
</script>
<style scoped>
textarea {
  outline: none;
}
.header_logo {
  width: 165px;
  height: 55px;
  margin-right: 20px;
}
.createPost {
  margin-bottom: 20px;
  padding: 10px 20px 10px 20px;
  display: grid;
  grid-template-rows: 1fr 2fr;
}
.profil_circle {
  position: relative;
  top: -60px;
}
.description {
  overflow-y: scroll;
  padding-left: 8px;
  width: 88%;
  height: 78px;
}
.tag {
  width: 30%;
  height: 30px;
}
.submit {
  font-weight: bold;
  position: relative;
  top: -14px;
  right: -7px;
  color: white;
}
</style>
