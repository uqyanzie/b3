<template>
  <div class="article-page d-flex">
    <div class="d-flex">
      <ArticleNavbar></ArticleNavbar>
      <div class="col col-xl article">
        <div class="container">
          <ShowArticle></ShowArticle>
        </div>
        <div class="right-bar">
          <SideBar></SideBar>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import ArticleNavbar from "../components/ArticleNavbar.vue";
import ShowArticle from "../components/ShowArtikel.vue";
import SideBar from "../components/ReadSideBar.vue"
import axios from "axios";
export default {
  name: "App",
  components: {
    ArticleNavbar,
    ShowArticle,
    SideBar
  },
  data() {
    return {
      form: {
        id_artikel: "",
        id_user: "",
        cover_artikel: "",
        judul_artikel: "",
        deskripsi_artikel: "",
        isi_artikel: "",
      },
      speakData: {
        synth: window.speechSynthesis,
        validation: false,
      },
    };
  },
  methods: {
    getItem() {
      axios
        .get("http://localhost:3000/artikel/publish/ART00000000041")
        .then((response) => {
          this.form = response.data;
          console.log(this.form);
        })
        .catch((error) => {
          console.log("Error Get Data ", error);
        });
    },
    speak() {
      if (this.speakData.synth.speaking) {
        console.error("speechSynthesis.speaking");
        this.speakData.synth.cancel();
        return;
      }

      if (this.form.isi_artikel !== "") {
        this.speakData.validation = false;
        const data =
          "Judul : " +
          this.form.judul_artikel +
          "\n\n\n" +
          "Deskripsi : " +
          this.form.deskripsi_artikel +
          "\n\n\n" +
          "Isi : " +
          this.form.isi_artikel;
        let sInstance = new SpeechSynthesisUtterance(data);
        sInstance.lang = "id-ID";
        sInstance.pitch = "1.0";
        this.speakData.synth.speak(sInstance);
      } else {
        this.speakData.validation = true;
      }
    },
  },
  mounted() {
    this.getItem();
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.article-page {
  background-color: #309c9f;
  height: max-content;
  margin: 0;
}

.article {
  border-radius: 50px 0 0 0;
  background: #e5e5e5;
  display: inline-flex;
}

.right-bar {
  width: 35%;
  border-radius: 50px 0 0 0;
  background: #fff;
  position: relative;
}
</style>
