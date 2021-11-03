<template>
  <div>
    <main-header navsel="front"></main-header>
  <div class="hero-wrapper">
      <img
        src="@/assets/logo.png"
        class="logo"
        style="float: left; width: 20%"
      />
      <br></br>
      <h2>THE HOTEL PORJECT</h2>
      <h3>Convenience service for you.</h3>
      <p>
        <h5>Contact</h5>
        <i class="fas fa-user-circle">
          </i> Sittichok Tongtub &nbsp;&nbsp;<br></br>
        <i class="fas fa-envelope"></i><a href="mailto:Sittichokt62@nu.ac.th" style="color: #000000"> Sittichokt62@nu.ac.th </a><br></br>
        <i class="fas fa-phone"></i> 
        <a href="phoneto:064-2851896" style="color: #000000">064-2851869</a> 
      </p>
      <i class="fas fa-user-circle">
          </i> Natdanai Eiamkai &nbsp;&nbsp;<br></br>
        <i class="fas fa-envelope"></i> <a href="mailto:NatdanaiE62@nu.ac.th" style="color: #000000">NatdanaiE62@nu.ac.th </a><br></br>
        <i class="fas fa-phone"></i> 
        <a href="phoneto:064-2851896" style="color: #000000">091-0131838</a> 
      </p>
    </div>
  <div class="container-fluid">
      <div class="container">
        <div class="blog-wrapper">
          <h4><i class="far fa-star"></i> Recommend</h4>
          <hr />
          <center>
            <img
              src="../../assets/mandatory.png"
              width="30%"
              class="d-inline-block align-top"
              alt=""
              loading="lazy"
            /><img
              src="../../assets/mandatory1.jpg"
              width="30%"
              class="d-inline-block align-top"
              alt=""
              loading="lazy"
            /><img
              src="../../assets/mandatory2.jpg"
              width="30%"
              class="d-inline-block align-top"
              alt=""
              loading="lazy"
               />
                <br <img
              src="../../assets/mandatory3.jpg"
              width="30%"
              class="d-inline-block align-top"
              alt=""
              loading="lazy"
            /><img
              src="../../assets/mandatory4.jpg"
              width="30%"
              class="d-inline-block align-top"
              alt=""
              loading="lazy"
            /><img
              src="../../assets/mandatory6.jpg"
              width="30%"
              class="d-inline-block align-top"
              alt=""
              loading="lazy"
               />
          </center>
          <br /><br />          
           <ui>
            <h3>จุดเด่น </h3>
            <i class="fas fa-home">
          </i>   ขนาดห้อง: 20-23 ตารางเมตร &nbsp;&nbsp;
            <br /><br /> 
            <i class="fas fa-smoking-ban">
          </i>   ห้องปลอดบุหรี่ &nbsp;&nbsp;
          <br /><br /> 
            <i class="fas fa-shower">
          </i>   ฝักบัว &nbsp;&nbsp;
          <br /><br /> 
          <h3>ประเภทเตียง </h3>
          <i class="fas fa-bed"></i>  <i class="fas fa-bed">
          </i> 2 เตียงเดี่ยว &nbsp;&nbsp;
          <i class="fas fa-bed"></i>  
          </i> 1 เตียงใหญ่ &nbsp;&nbsp;
          <i class="fas fa-bed"></i>  
          </i> 1 เตียงเดี่ยว &nbsp;&nbsp;
           <br /><br /> 
          <h3>ห้องน้ำและอุปกรณ์ในห้องน้ำ </h3>
          <i class="fas fa-shower"></i> 
          </i> ของใช้ในห้องน้ำ &nbsp;&nbsp;
            <i class="fas fa-point">
          </i>   ผ้าเช็ดตัว &nbsp;&nbsp;
           <br /><br /> 
          <h3>ความบันเทิง </h3>
          <i class="fas fa-signal">
          </i>   Wi-Fi ทุกห้อง (ฟรี) &nbsp;&nbsp;
          <i class="fas fa-tv">
          </i>   โทรทัศน์ดาวเทียม/เคเบิล &nbsp;&nbsp;
          <br></br>
            <i class="fas fa-phone"></i> 
            </i>  โทรศัพท์ &nbsp;&nbsp;
              <br /><br /> 
          <h3>สิ่งอำนวยความสะดวก </h3
          <i class="fas fa-snowflake"></i>
            </i>  เครื่องปรับอากาศ &nbsp;&nbsp;
             <i class="fas fa-fridge"></i>
            </i>  ตู้เย็น &nbsp;&nbsp;
            <br /><br /> 
          <h3>อาหาร เครื่องดื่ม ของว่าง</h3
          <i class="fas fa-mug-hot">
          </i>   กาแฟ/ชา &nbsp;&nbsp;
          <i class="fas fa-tint">
          </i>   น้ำดื่มบรรจุขวด (ฟรี) &nbsp;&nbsp;
          <br></br>
          <h3>บริการและสิ่งอำนวยความสะดวก</h3
            <i class="fas fa-broom">
          </i>  บริการทำความสะอาดรายวัน &nbsp;&nbsp;
            </ui>  
            </ui>            
        </div>
        <div class="footer"></div>
      </div>
    </div>
  </div>
</template>
<script>
import BlogsService from "@/services/BlogsService";
import _ from "lodash";
import ScrollMonitor from "scrollMonitor";
let LOAD_NUM = 3;
let pageWatcher;
export default {
  watch: {
    search: _.debounce(async function (value) {
      const route = {
        name: "front",
      };
      if (this.search !== "") {
        route.query = {
          search: this.search,
        };
      }
      console.log("search: " + this.search);
      this.$router.push(route);
    }, 700),
    "$route.query.search": {
      immediate: true,
      async handler(value) {
        this.blogs = [];
        this.results = [];
        this.loading = true;
        this.results = (await BlogsService.index(value)).data;
        this.appendResults();
        this.results.forEach((blog) => {
          if (this.category.length > 0) {
            // console.log(this.category.indexOf(blog.category))
            if (this.category.indexOf(blog.category) === -1) {
              this.category.push(blog.category);
          }
          } else {
            this.category.push(blog.category);
          }
        });
        this.loading = false;
        this.search = value;
        // console.log(this.category)
      },
    },
  },
  data() {
    return {
      blogs: [],
      BASE_URL: "http://localhost:8081/assets/uploads/",
      search: "",
      results: [],
      category: [],
      loading: false,
    };
  },
  // async created () {
  // this.blogs = (await BlogsService.index()).data
  // },
  methods: {
    appendResults: function () {
      if (this.blogs.length < this.results.length) {
        let toAppend = this.results.slice(
          this.blogs.length,
          LOAD_NUM + this.blogs.length
        );
        this.blogs = this.blogs.concat(toAppend);
      }
    },
    navigateTo(route) {
      this.$router.push(route);
    },
    async deleteBlog(blog) {
      try {
        await BlogsService.delete(blog);
        this.refreshData();
      } catch (err) {
        console.log(err);
      }
    },
    async refreshData() {
      this.blogs = (await BlogsService.index()).data;
    },
    setCategory(keyword) {
      if (keyword === " ") {
        this.search = "";
        console.log("null");
      } else {
        this.search = keyword;
      }
    },
  },
  updated() {
    let sens = document.querySelector("#blog-list-bottom");
    pageWatcher = ScrollMonitor.create(sens);
    pageWatcher.enterViewport(this.appendResults);
  },
  beforeUpdated() {
    if (pageWatcher) {
      pageWatcher.destroy();
      pageWatcher = null;
    }
  },
};
</script>
<style scoped>
.component-wrapper {
  padding-left: 5px;
  padding-right: 5px;
}
.hero-wrapper {
    margin-top: 40px;
  max-width: 1100px;
  margin-left: auto;
  margin-right: auto;
  border-radius: 5px;
  background: linear-gradient( 45deg, #ffa69e, #faf3dd, #b8f2e6, #aed9e0, #5e6472);
  height: auto;
  color: #000000;
  padding: 20px;
}
.hero h1 {
  margin-top: 30px;
}
.logo {
  padding-right: 20px;
}
.empty-blog {
  width: 100%;
  text-align: center;
  padding: 10px;
  background: rgb(196, 50, 50);
  color: white;
}
/* thumbnail */
.thumbnail-pic img {
  width: 200px;
  padding: 5px 5px 5px 5px;
  border: solid 1px #ccc;
  margin: 10px 10px 0px 0px;
}
.blog-info {
  float: left;
}
.blog-pic {
  float: left;
}
.clearfix {
  clear: both;
}
.blog-list {
  border: solid 1px #dfdfdf;
  margin-bottom: 10px;
  max-width: 900px;
  margin-left: auto;
  margin-right: auto;
  padding: 5px;
  box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.1);
}
.blog-header {
  margin-top: 80px;
  max-width: 900px;
  margin-left: auto;
  margin-right: auto;
}
#blog-list-bottom {
  padding-top: 4px;
}
.blog-load-finished {
  padding: 4px;
  text-align: center;
  background: seagreen;
  color: white;
}
.categories {
  margin-top: 20px;
  padding: 0;
  list-style: none;
  float: left;
}
.categories li {
  float: left;
  padding: 2px;
}
.categories li a {
  padding: 5px 10px 5px 10px;
  background: paleturquoise;
  color: black;
  text-decoration: none;
}
.categories li.clear a {
  background: tomato;
  color: white;
}
.create-blog {
  margin-top: 10px;
}
@media (max-width: 768px) {
  .logo {
    width: 120px;
  }
}
.header {
  margin-left: auto;
  margin-right: auto;
  margin-top: 0px;
  padding: 10px;
  position: relative;
  background-color: #ececec;
  border-bottom: 1px solid rgba(255, 255, 255, 0.5);
  box-shadow: 0 -2px 1px rgba(0, 0, 0, 0.1) inset;
  text-shadow: 1px 1px 1px #fff;
}
.categories {
  margin-top: 10px;
  padding: 0;
  width: 100%;
}
.blog-wrapper {
  margin-top: 20px;
  padding: 40px;
  height: 100%;
  background: #f1f1f2;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}
.blog-tab {
  padding: 1px;
  background-color: #d3d3d3;
  text-align: left;
  text-indent: 0.5em;
}
.footer {
  margin-top: 50px;
}
</style>