<template>
  <div class="container container-block">
    <Header></Header>
    <div class="row portfolio-section mt-3 mb-3">
      <div class="col">
        <h3>My Portfolio's</h3>
        <br/>
        <div class="row mt-3 pl-3">
          <div class="col col-12 border-left border-secondary p-2 mt-4 mb-4" v-for="portfolio in portfoliosList" :key="portfolio._id" >
            <h4>{{ portfolio.title }}</h4>
            <p class="mt-2 mb-0"><b class="mr-2">Development Tools:</b> {{ portfolio.description }}</p>
            <p class="mt-0 mb-0"><b class="mr-2">Web Address:</b> <a :href="portfolio.url" target="_blank"> {{ portfolio.url }}</a></p>
          </div>
        </div>
      </div>
    </div>
    <Footer></Footer>
  </div>
</template>

<script>
import Header from './../../../components/common/Header.vue'
import Footer from './../../../components/common/Footer.vue'
export default {
  name: "portfoliolist",
  components: {
    Header,
    Footer
  },

  data () {
    return {
      portfoliosList: []
    }
  },

  methods: {
    getAllPortfolios() {
      this.axios
      .get(
        `${process.env.VUE_APP_AWESOME_NODE_API}/portfolios/`,
      )
      .then(res => {
        this.portfoliosList = res.data.data;
      })
      .catch(err => {
        console.log(err);
      });
    }
  },

  mounted() {
    this.getAllPortfolios();
  }
  
}
</script>

<style scoped lang="scss">
  .portfolio-section {
    h3 {
      color: #000;
      font-weight: bold;
    }
  }
</style>