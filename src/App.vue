<template>
  <div>
    <Header />
    <div class="container">
      <div class="row">
        <div class="col-md-5">
          <h3>Enter your personal data</h3>
          <form>
            <div class="form-group">
              <label for="fullname">Full Name:</label>
              <input
                type="name"
                class="form-control"
                id="fullname"
                placeholder="Enter full name"
                v-model="name"
              />
            </div>
            <div class="form-group">
              <label for="proffesion">Proffesion:</label>
              <input
                type="text"
                class="form-control"
                id="proffesion"
                placeholder="Enter proffesion"
                v-model="proffesion"
              />
            </div>
            <div class="form-group">
              <label for="phone">Phone:</label>
              <input
                type="text"
                class="form-control"
                id="phone"
                placeholder="Enter phone"
                v-model="phone"
              />
            </div>
            <div class="form-group">
              <label for="email">Email:</label>
              <input
                type="text"
                class="form-control"
                id="email"
                placeholder="Enter email"
                v-model="email"
              />
            </div>
            <div class="form-group">
              <label for="linkedin">Linkedin:</label>
              <input
                type="text"
                class="form-control"
                id="linkedin"
                placeholder="Enter linkedin"
                v-model="linkedin"
              />
            </div>
            <label for="linkedin">Upload Image:</label>
            <div class="input-group mb-3">
              <div class="custom-file">
                <input type="file" class="custom-file-input" id="profile" @change="onFileSelected" />
                <label class="custom-file-label" for="profile">{{fileName}}</label>
              </div>
            </div>
          </form>
        </div>
        <div class="col-md-7">
          <div class="card-container" id="my-card">
            <div class="left-side">
              <h3>{{name}}</h3>
              <span>{{proffesion}}</span>
              <div class="contact">
                <p>
                  <i class="fa fa-phone-square mr-2" style="font-size:21px"></i>
                  {{phone}}
                </p>
                <p>
                  <i class="fa fa-envelope mr-2"></i>
                  {{email}}
                </p>
                <p>
                  <i class="fa fa-linkedin-square mr-2" style="font-size:21px"></i>
                  {{linkedin}}
                </p>
              </div>
            </div>
            <div class="break-line"></div>
            <div class="right-side">
              <img :src="selectedFile" width="100" height="100" />
            </div>
          </div>
          <button type="button" class="btn btn-success mt-4" @click="download">Download Card</button>
          <h4 class="text-center mt-3" v-if="isDownloading">Downloading card...</h4>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Header from "@/components/Header";
import htmlToImage from "html-to-image";
import download from "downloadjs";
import defaultImage from "./assets/john.jpg";

export default {
  name: "App",
  components: {
    Header
  },
  data: () => ({
    name: "Joh Doe",
    proffesion: "Software Developer",
    phone: "+35568123456",
    email: "johndoe@gmail.com",
    linkedin: "Joh Doe",
    selectedFile: defaultImage,
    fileName: "Choose Image",
    isDownloading: false
  }),
  methods: {
    download() {
      this.isDownloading = true;
      htmlToImage
        .toPng(document.getElementById("my-card"))
        .then(dataUrl => {
          this.isDownloading = false;
          download(dataUrl, "my-card.png");
        })
        .catch(err => {
          this.isDownloading = false;
          console.log(err);
        });
    },
    onFileSelected(e) {
      if (!e.target.files[0]) {
        return;
      }
      if (!e.target.files[0].name.match(/.(jpg|jpeg|png)$/i)) {
        alert("File is not an image! Please choose an image.");
        return;
      }
      this.selectedFile = URL.createObjectURL(e.target.files[0]);
      this.fileName = e.target.files[0].name;
    }
  }
};
</script>
<style scoped>
.card-container {
  width: 550px;
  display: flex;
  border: 2px solid rgb(14, 33, 63);
}
a {
  color: white;
}
p {
  margin: 0;
}
.left-side {
  position: relative;
  width: 300px;
  height: 220px;
  padding: 10px 20px 10px 10px;
  font-size: 20px;
  position: relative;
  color: #fff;
  background: rgb(14, 33, 63);
}
.left-side:after {
  content: " ";
  position: absolute;
  display: block;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  z-index: -1;
  background: rgb(14, 33, 63);
  transform-origin: bottom left;
  -ms-transform: skew(-30deg, 0deg);
  -webkit-transform: skew(-30deg, 0deg);
  transform: skew(-30deg, 0deg);
}
.break-line {
  width: 10px;
  height: 220px;
  margin-left: 66px;
  transform: skew(-30deg, 0deg);
  background: #1565c0;
}
.right-side {
  display: flex;
  margin-left: 50px;
  align-items: center;
}
.right-side img {
  border-radius: 50%;
}
form {
  width: 80%;
}
.left-side span {
  font-size: 18px;
  color: #ddd1d1;
}
.left-side .contact {
  margin-top: 22px;
}
.left-side .contact p {
  display: flex;
  align-items: center;
  font-size: 18px;
}
</style>
