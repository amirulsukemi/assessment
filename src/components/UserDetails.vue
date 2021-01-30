<template>
  <div class="user-card">

    <a class="btn-filter" v-on:click="isHidden = !isHidden">
			<img src="../assets/img/btn-filter.png"> <span class="btn-text">Filter</span>
		</a>

    <div class="search-box"><button class="btn-search"></button></div><input type="text" v-model="searchValue" class="search-input" placeholder="Search Full Name">
    <div class="clearfix"></div>

    <div class="filter-container" v-if="!isHidden">
      <p>Sort by:</p>
      <div class="filter-box">
        <div class="filterbox1" @click="sort('name')">Name</div>
        <div class="filterbox2" @click="sort('username')">Username</div>
      </div>
      
    </div>

    <ul>
    <li v-for="userdetails in filteredUsers" :key="userdetails">
      <div class="user-card-details">
        <div class="icon"><img :src="userdetails.profile_picture"></div>
        <div class="user-card-content">
          <div class="border">ID : {{userdetails._id.$oid}}</div>
          <div class="border">Username : {{ userdetails.username }}</div>
          <div class="border">Password : {{ userdetails.password }}</div>
          <div class="border">Full Name: {{ userdetails.name }}</div>
          <div class="border">Email : {{ userdetails.email }}</div>
          <div class="border">Register Date : {{ userdetails.register_date }}</div>
        </div>
      </div>
    </li>
    </ul>
  </div>
</template>

<script>
import json from "../assets/USER_DATA.json";
export default {
  name: "UserDetails",
  data(){
    return{
      sortKey:'',
      reverse: false,
      currentSort:'',
      currentSortDir:'asc',
      searchValue: '',
      sortRegisterDate: '',
      isHidden: true,
      userdata: json
    }
  },
  methods:{
    sort:function(s) {
      if(s === this.currentSort) {
        this.currentSortDir = this.currentSortDir==='asc'?'desc':'asc';
      }
      this.currentSort = s;
    }
  },
  computed: {
    filteredUsers() {
        let tempuserdata = this.userdata

        // search input
        if (this.searchValue != '' && this.searchValue) {
          tempuserdata = tempuserdata.filter((item) => {
            return item.name
              .toUpperCase()
              .includes(this.searchValue.toUpperCase())
          })
        }

        // Sort full name by alphabetical order
        tempuserdata = tempuserdata.sort((a, b) => {
          let modifier = 1;
          if(this.currentSortDir === 'desc') modifier = -1;
          if(a[this.currentSort] < b[this.currentSort]) return -1 * modifier;
          if(a[this.currentSort] > b[this.currentSort]) return 1 * modifier;
          return 0;
        })
  
        return tempuserdata
    }

  }
};
</script>

<style scoped>
h1, h2 {font-weight: normal;}
ul {list-style-type: none;padding: 0;}
li {width: 25%;float: left;}
a { color: #42b983;}
.user-card {max-width: 900px; margin: auto;}
.user-card-details {margin: 10px;height: 300px;}
.icon {height: 150px;margin: auto;}
.icon img {width: 100%; height: 100%;}
.user-card-content {border: 1px solid #ef4232; border-radius: 0px 0px 10px 10px; border-top: 0px;padding: 20px 10px; font-size: 12px;}
.border {border-bottom: 1px solid #ef4232;}

.btn-filter {border: 1px solid #EF4233; border-radius: 35px;font-weight: bold;letter-spacing: 1px;color: #EF4233;margin: 35px 10px 25px;padding: 10px 20px;display: inline-flex;align-items: center;float: left;}
.btn-filter img {height: 22px;}
.btn-text {padding: 0 13px 0 10px;}
.btn-search {float:right;background: none;height: 28px;width: 28px;border-radius: 100%;outline: 0;color: inherit;-webkit-transition: 0.2s ease-in-out;transition: 0.2s ease-in-out;border: 5px solid #ef4233;cursor: pointer;}
.btn-search:before {content: "";position: absolute;width: 10px;height: 5px;background-color: #ef4233;-webkit-transform: rotate(45deg);-ms-transform: rotate(45deg);transform: rotate(35deg);margin-top: 7px;margin-left: 10px;}
.search-input {float: right;margin: 35px 0px 25px;padding: 12px;border: #ecedf0 1px solid; -webkit-border-top-left-radius: 40px;-webkit-border-bottom-left-radius: 40px;-moz-border-radius-topleft: 40px;-moz-border-radius-bottomleft: 40px;border-top-left-radius: 40px;border-bottom-left-radius: 40px; outline: none;background-color: #ecedf0; font-size: 14px;letter-spacing: 0.3px; line-height: 20px; color: #5F6062;}
.search-box {border: 1px solid #ecedf0;float: right;margin: 35px 12px 25px 0; padding: 8px; background: #ecedf0; border-top-right-radius: 40px; border-bottom-right-radius: 40px;}

.filter-container {border-radius: 10px;margin: 0 10px 22px;padding: 20px;background: #ecedf0; font-weight: bold;color: #ef4232;}
.filter-container p {padding: 15px; text-align: left;}
.filter-box{display: flex;flex-wrap: nowrap;margin-top: 20px;}
.filterbox1 {margin-right: 23px;cursor: pointer;padding: 15px;}
.filterbox1:hover {border: 1px solid #EF4233;border-radius: 10px;background-color: red; color: #ffffff;}
.filterbox2 {cursor: pointer;padding: 15px;}
.filterbox2:hover {border: 1px solid #EF4233;border-radius: 10px;background-color: red; color: #ffffff;}

@media only screen and (max-width: 600px) {

  li {width: 100%;}

  .search-input {padding: 12px 0 12px 5px;font-size: 10px;width: 100px;}
  .search-box {padding: 8px 8px 8px 0;}

}
</style>
