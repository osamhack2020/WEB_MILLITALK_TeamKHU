<template>
  <v-app id="inspire">
    <v-app-bar app color="white" flat>
      <v-container class="py-0 fill-height">
        <img class="header_logo" src="../assets/logo.png" />

        <v-btn v-for="link in links" :key="link" text>
          {{ link }}
        </v-btn>
        <v-btn><v-icon>mdi-account</v-icon></v-btn>
        <v-btn><v-icon>mdi-bell</v-icon></v-btn>
        <v-btn><v-icon>mdi-home</v-icon></v-btn>
        <v-btn><v-icon>mdi-chat</v-icon></v-btn>
        <v-spacer></v-spacer>

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
            <v-sheet min-height="70vh" rounded="lg">
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
    links: ["메인", "채팅", "알림", "프로필"],
    board: ["군생활", "연애", "부조리", "건의사항", "운동", "기타"]
  })
};
</script>
<style scoped>
.header_logo {
  width: 180px;
  height: 60px;
  margin-right: 20px;
}
</style>
