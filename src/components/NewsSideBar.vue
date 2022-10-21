<script >
import {APISettings} from '../components/api.js';
export default {
  data() {
    return {
      newsType: 'News Info',
      getResult:null,
      showNav: false,
    }
  },
  methods: {
    async getNews(data) {
      this.toggle();
      this.newsType=data;
      let newsValue=this.getSelectedNews(data);
      await fetch(APISettings.baseURL+newsValue+"&apiKey=a65429315e8a4bd58644f190c2af875b" , {
				method: 'GET'
    })
    .then( function( response ){
      return response.json();
    }).then((result) => {
    this.getResult = result.articles;
    }).catch((error) => {
    console.error('Error:', error);
  });
  },
    dateFormat(data) {
      return new Date(data).toGMTString().replace('GMT','');
  },
  toggle() {
      this.showNav = !this.showNav
    },
getSelectedNews(newType){
  switch(newType){
    case "Top News":
      return '';
      break;
    case "Business":
      return "&category=business";
      break;
    case "Entertainment":
      return '&category=entertainment';
      break;
    case "Health":
      return '&category=health';
      break;
    case "Science":
      return '&category=science';
      break;
    case "Sports":
      return '&category=sports';
      break;
    case "Technology":
      return '&category=technology';
      break;
    default:
      return '';
  }
  
}
},
beforeMount(){
    this.getNews('Top News');
 }
}
</script>
<template>
  
  <div class="news-container">
    <div class="news-list" >
    <nav class="demo-navigation mdl-navigation mdl-color--blue-grey-900" :class="{hide: showNav}">
          <div class="mdl-navigation__link" @click="getNews('Top News')"><i class="mdl-color-text--red-400 material-icons" role="presentation">equalizer</i><span> TOP NEWS</span></div>
          <div class="mdl-navigation__link" @click="getNews('Business')"><i class="mdl-color-text--red-400 material-icons" role="presentation">business_center</i> BUSINESS</div>
          <div class="mdl-navigation__link" @click="getNews('Entertainment')"><i class="mdl-color-text--red-400 material-icons" role="presentation">music_video</i> ENTERTAINMENT</div>
          <div class="mdl-navigation__link" @click="getNews('Technology')"><i class="mdl-color-text--red-400 material-icons" role="presentation">settings_system_daydream</i> TECHNOLOGY</div>
          <div class="mdl-navigation__link" @click="getNews('Science')"><i class="mdl-color-text--red-400 material-icons" role="presentation">public</i> SCIENCE</div>
          <div class="mdl-navigation__link" @click="getNews('Sports')"><i class="mdl-color-text--red-400 material-icons" role="presentation">directions_run</i> SPORTS</div>
          <div class="mdl-navigation__link" @click="getNews('Health')"><i class="mdl-color-text--red-400 material-icons" role="presentation">local_hospital</i> HEALTH</div>
        </nav>
  </div>
  
  <div class="news-content">
    <button class="btn btn-outline-info float-end mt-1" @click="toggle" type="button">
      Show News Menu
    </button>
    <div class="news-list-view mt-5">
      <h3>{{newsType}}</h3>
      <div class="row">
        <div class="col-sm-6" v-for="newsResult in getResult">
          <div class="card my-3">
            <img v-if="newsResult.urlToImage == null" src="https://via.placeholder.com/150" height="300">
            <img v-else :src="newsResult.urlToImage" class="card-img-top" alt="..." height="300">
            <div class="card-body">
              <h5 class="card-title">{{newsResult.title}}</h5>
              <p class="card-text" v-if="newsResult.description == null">{{newsResult.content}}</p>
              <p class="card-text" v-else>{{newsResult.description}}</p>
              <a :href="newsResult.url" target="_blank" class="card-link">Know more</a>
              <span class="card-link">Posted On: {{dateFormat(newsResult.publishedAt)}}</span>
            </div>
          </div>
        </div>
      </div>
    </div>


  </div>
  </div>
</template>

<style>
.demo-navigation {
  height: 100%;
  width: 220px;
  position: fixed;
  z-index: 1;
  top: 50px;
  left: 0;
  background-color: rgb(243 240 240);
  overflow-x: hidden;
  padding-top: 20px;
}

.news-container{
    display: flex;
    width: 100%;
}
.news-list{
  width: 20%;
}
.news-content{
  width: 75%;
}

.demo-navigation div{
  padding: 15px;
}
.demo-navigation div:hover{
  background: #c9c5c5;
  cursor: pointer;
}
.demo-navigation div .material-icons{
  float: left;
  padding-right: 10px;
}
.hide{
  display: none;
}
</style>