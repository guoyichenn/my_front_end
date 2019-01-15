<template>
  <div class="linkage">
    <el-select v-model="province" @change="choseProvince" placeholder="省级地区">
      <el-option v-for="item in provinces" :key="item.id" :label="item.value" :value="item.id"></el-option>
    </el-select>
    <el-select v-model="city" @change="choseCity" placeholder="市级地区">
      <el-option v-for="item in citys" :key="item.id" :label="item.value" :value="item.id"></el-option>
    </el-select>
    <el-select v-model="country" @change="choseBlock" placeholder="区级地区">
      <el-option v-for="item in countrys" :key="item.id" :label="item.value" :value="item.id"></el-option>
    </el-select>
  </div>
</template>

<script>

export default {
  data() {
    return {
      mapJson: "../static/json/map.json",
      provinces: [],
      citys: [],
      countrys: [],
      province: "",
      city: "",
      country: "",
      init: true
    };
  },
  methods: {
    // 加载china地点数据，三级
    getProvinceData: function() {
      let p = [
        {
          id: 1,
          value: "北京"
        },
        {
          id: 2,
          value: "上海"
        },
        {
          id: 3,
          value: "广州"
        }
      ];
      this.provinces = p;
    },
    // 选省
    choseProvince: function() {
      this.citys = [];
      this.city = "";
      this.countrys = [];
      this.country = "";
      switch (this.province) {
        case 1:
          this.citys = [{ id: 10, value: "朝阳" }];
      }
    },
    // 选市
    choseCity: function() {
      this.countrys = [];
      this.country = "";
      switch (this.city) {
        case 10:
          this.countrys = [{ id: 100, value: "潘家园" }];
      }
    },
    // 选区
    choseBlock: function() {},
    initData : function(data){
        this.province = data.province.id;
        this.choseProvince();
        this.city = data.city.id;
        this.choseCity();
        this.country = data.country.id;
    }
  },
  created: function() {
    this.getProvinceData();
    if (this.init) {
        let initData = {
            province : {
                id : 1,
                value : "北京"
            },
            city : {
                id : 10,
                value : "朝阳"
            },
            country : {
                id : 100,
                value : "潘家园"
            },
        }
        this.initData(initData);
    }
  }
};
</script>

<style scoped>
</style>

