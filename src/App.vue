<template>
  <div>
    <Header />
    <div class="container">
      <div class="row">
        <div class="col-md-5">test</div>
        <div class="col-md-7"><div class="card-container">
        <div class="left-side">
          <a href="#">Baustellenbedarf</a>
          <p>Hello World</p>
          <p>Hsfdsf</p>
        </div>
        <div class="break-line"></div>
        <div class="right-side">sdfsdddf</div>
      </div></div>
      </div>
      
    </div>
  </div>
</template>

<script>
import Header from "@/components/Header"
export default {
  name: "App",
  components:{
    Header
  },
  data: () => ({
  
  })
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
.right-side{
  display: flex;
  margin-left: 70px;
  align-items: center;
}
</style>
