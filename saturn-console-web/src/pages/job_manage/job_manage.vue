<template>
    <div>
        <el-main>
            <div class="page-home">
              <div class="page-home-container">
                  <div class="page-title">
                      <img width="200px" height="200px" src="../../image/saturn.png"/>
                  </div>
                  <div>
                      <el-autocomplete
                        v-model="domainName"
                        :fetch-suggestions="querySearchAsync"
                        placeholder="请输入域名"
                        @select="handleSelect"
                        style="width: 600px;">
                      <i class="el-icon-search el-input__icon" slot="suffix"></i>
                      </el-autocomplete>
                  </div>
              </div>
            </div>
        </el-main>
    </div>
</template>

<script>
export default {
  data() {
    return {
      domainName: '',
      domains: this.$store.getters.allDomains,
    };
  },
  methods: {
    querySearchAsync(queryString, cb) {
      const domains = this.domains;
      const results = queryString ? domains.filter(this.createStateFilter(queryString)) : domains;
      cb(results);
    },
    createStateFilter(queryString) {
      return state =>
        state.value.toLowerCase().indexOf(queryString.toLowerCase()) >= 0;
    },
    handleSelect(item) {
      this.toJobListPage(item.value);
    },
    toJobListPage(domain) {
      this.$router.push({ name: 'job_overview', params: { domain } });
    },
  },
};
</script>
<style lang="sass" scoped>
.page-home {
    width: 600px;
    margin: 0 auto;
    .page-home-container {
        margin-top: 22%;
        .page-title {
            font-size: 19px;
            font-weight: normal;
            margin: 10% 0 0;
            text-align: center;
            color: #159e74;
        }
    }
}
</style>
