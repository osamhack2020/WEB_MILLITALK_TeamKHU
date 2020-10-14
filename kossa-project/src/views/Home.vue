<template>
  <v-app id="inspire">
    <v-app-bar color="white" flat>
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
                label="Tag"
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
              <div class="post" v-for="(post, index) in posts" :key="index">
                <div class="postMain">
                  <v-icon class="profilIcon" size="60"
                    >mdi-account-circle</v-icon
                  >
                  <div class="postText">
                    <div>
                      <sapn class="postWriter">해군참치</sapn> |
                      <span class="postTag">#군생활</span> |
                      <span class="postTime">2시간 전</span>
                    </div>
                    <div class="postContent">{{ post }}</div>
                  </div>
                </div>
                <v-divider></v-divider>
                <div class="postFooter">
                  <v-btn text><v-icon color="red">mdi-heart</v-icon></v-btn>
                  <v-btn text><v-icon color="blue">mdi-message</v-icon></v-btn>
                </div>
              </div>
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
    new_posts_tag: "",
    current_user: {},
    posts: [
      "자바스크립트를 한마디로 요약하자면 웹을 풍부하게 만들어주는 작고 가벼운 언어입니다. 미국의 넷스케이프 커뮤니케이션즈사(Netscape Communications)가 개발한 스크립트 언어이며. 웹 브라우저에서 실행하는 스크립트 언어를 기술합니다. 작고도 빠르기 때문에 웹문서를 동적으로 꾸밀 때 가장 널리 쓰입니다. 언어 규격은 자바의 부분 집합(subset)으로 되어 있습니다. 하이퍼텍스트 생성 언어(HTML) 문서를 작성하는 수준의 사용자가 사용하는 것을 주안점으로 하여 자바의 언어 규격으로부터 변수의 형(정수형이나 문자열형 등)을 생략하거나 새로운 클래스 정의를 할 수 없도록 하였습니다. 스크립트는 HTML 문서 속에 직접 기술하며, ‘<script>’라는 꼬리표를 사용합니다. 프로그래밍 입문자들은 자바스크립트와 자바가 서로 비슷한 기술이라고 생각하곤 합니다. 두 언어 모두 자바라는 언어를 기반으로 하고 있기 때문이죠. 하지만 자바스크립트는 자바와는 다른점이 상당히 많습니다. 기능과 사용법까지 완전히 다릅니다.",
      `이 문서도 역시 엄연한 웹 페이지이며, 따라서 현재 이 문서를 읽고 있다면 '웹 페이지를 보고 있다'고도 할 수 있습니다.
그리고 이 web 이란 용어는 인터넷과 동의어로 쓰이는 경우가 많으나 엄격히 말해 서로 다른 개념입니다.

인터넷이란 이름은 '네트워크의 네트워크'를 구현하여 모든 컴퓨터를 하나의 통신망 안에 연결(Inter Network)하고자 하는 의도에서

이를 줄여 인터넷(Internet)이라고 처음 명명하였던데 어원을 두고 있습니다.

이러한 개념들을 상세히 숙지하고 있을 필요는 없지만 이 분야를 공부하고자 한다면 배경 지식정도는 알아두면 좋을 것 같습니다.

또한 앞으로 이 마크업 언어를 숙지하는데 있어 항상 시멘틱 마크업을 목표로 나아가야 할 것입니다.
시멘틱 마크업(Semantic Markup) 은 웹 사이트(페이지)의 콘텐츠를 설명하는데 사용되는 마크업 언어이고,
HTML 은 콘텐츠의 의미를 설명하는데 유일한 목적을 가집니다.
앞으로 공부할 CSS 가 비주얼 디자인(Visual Design) 이라면 HTML 은 구조적 설계(Structure Design) 이라 할 수 있습니다.
`,
      "휴가 나가고 싶다",
      "코로나 위로휴가 주세요",
      "일하기 싫다",
      "전역 언제하냐..",
      "이제 52퍼다..",
      "목아프다"
    ]
  }),
  mounted() {
    this.$firebase.auth().onAuthStateChanged(user => {
      if (user) {
        let User = this.$firebase.auth().currentUser;
        this.current_user.name = User.displayName;
        this.current_user.email = User.email;
        this.current_user.photoUrl = User.photoURL;
        this.current_user.emailVerified = User.emailVerified;
        this.current_user.uid = User.uid;
        console.log(this.current_user);
      } else {
        this.$router.replace("/login");
      }
    });
  },
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
.header,
.v-toolbar__content {
  box-shadow: 0 0 20px rgb(0, 0, 0, 0.2);
  border-bottom: 1px solid black;
}
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
.postsBoard {
  padding: 20px;
}
.post {
  width: 100%;
  box-shadow: 0 0 20px rgb(0, 0, 0, 0.2);
  border-bottom: 1px solid #a5a3a3;
  border-left: 1px solid #ccc6c6;
  border-radius: 5px;
  padding: 10px;
  margin-bottom: 20px;
}
.postMain {
  display: grid;
  grid-template-columns: 1fr 12fr;
}
.postFooter {
  height: 25px;
  display: grid;
  grid-template-columns: 1fr 1fr;
}
.postWriter {
  display: inline-block;
  font-weight: bold;
}
.postTag,
.postTime {
  color: grey;
  font-size: 14px;
}
.postText {
  padding: 10px;
  padding-top: 10px;
  overflow: hidden;
}
.postContent {
  font-size: 13px;
}
</style>
