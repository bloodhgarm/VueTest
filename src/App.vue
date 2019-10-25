<template>
  <div id="app">
    <div class="container">
      <nav class="navbar navbar-expand-xs">
        <button class="navbar-toggler mr-5" type="button" @click="show = !show">
        </button>
        <a class="navbar-brand" href="#">Company logo</a>
        <div class="ml-auto dropdown">
                <button class="btn btn-secondary dropdown-toggle" type="button" id="dropdownMenuButton" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
                    Option
                </button>
                <div class="dropdown-menu" aria-labelledby="dropdownMenuButton">
                    <a class="dropdown-item" href="#">Eng</a>
                    <a class="dropdown-item" href="#">Rus</a>
                </div>
        </div>
      </nav>
      <div class="row b-content">
        <div class="side-bar col-6 col-sm-6 col-md-4 col-lg-3" :class="{'side-bar__hidden': !show}">
          <ul class="sidebar-nav">
              <li v-for="listItem in list" :key="listItem._id">
                  <button type="button" @click="currentUserID = listItem._id">{{listItem.friends[0].name}}</button>
              </li>
          </ul>
        </div>
        <div class="col-lg-9 col col-md-12" :class="{'col-12 col-lg-12': !show}">
          <div class="row">
            <div class="col-lg-3 col-md-5 d-none d-md-block b-white ">
              <ul>
                <li v-for="item in currenUser.friends" :key="item.id" class="media"><img src="./assets/img/icon-round.png" class="mr-3" alt="..."> <div class="media-body">{{item.name}} </div></li>
              </ul>
            </div>
            <div class="col b-gray ">
                <p class="about" v-html="currenUser.about"></p>
            </div>
            <div class="col-lg-3 d-none d-lg-block b-white ">
              <div class="description" v-html="currenUser.description"></div>
            </div>
          </div>
        </div>
      </div>
      <footer  class="footer mt-auto">
        <div class="row align-items-center">
            <div class="col"><span class="text-light">© Copyright 2017</span></div>
            <div class="col">
              <button type="button" name="" id="" class="btn btn-save" btn-lg btn-block><i class="far fa-save"></i>Save</button>
              <button type="button" name="" id="" class="btn btn-back" btn-lg btn-block><i class="fas fa-share"></i>Back</button>
            </div>
        </div>
      </footer>
    </div>
  </div>
</template>

<script>
import list from '@/assets/generated.json';
export default {
  name: 'app',
  components: {
  },
  data() {
    return {
      show: true,
      list,
      currentUserID: 0,
    };
  },
  computed: {
    currenUser(){
      for (let index = 0; index < this.list.length; index++) {
        const element = this.list[index];
        if (index == this.currentUserID) {
          return element;
        }
        
      }
      return this.list[0]
    },
  },
}
</script>

<style lang="scss">
  @import './assets/bootstrap/bootstrap.scss';
  *{
    box-sizing: border-box;
  }
  #app{
    height: 100vh;
  }
  .container{
    overflow: hidden;
    position: relative;
    height: 100%;
  }
  .side-bar{
    transform: none;
    transition: 100ms;
    overflow-y: auto;
    max-height: 100%;
    overflow-x: hidden;
  }
  .sidebar-nav {
    position: absolute;
    top: 0;
    margin: 0;
    width: 100%;
    padding: 0;
    list-style: none;
    background-color: #7000e0;
    
    li:hover{
     background-color: #9347df;
    }
    button{
      border: none;
      background-color: transparent;
      color: white;
      width: 100%;
      height: auto;
      padding: 15px;

    }
  }
  .navbar{
      background-color: #7e00ff;
      a{
        color: white;
      }
      .navbar-toggler{
        background-color: #fff;
        background-image: url(./assets/img/burger.png);
        background-repeat: no-repeat;
        background-position: center center;
        width: 50px;
        height: 40px;

      }
      .dropdown-toggle{
        background-color: #fff;
        color: #7e00ff;
      }
      .dropdown-menu{
        left: -70%;
        a{
           color: #7e00ff;
        }
      }
  }
  .b-content{
    height: 700px;
    max-width: 1110px;
    .b-gray{
      background-color: #e6e6e6;
      color: #3c3c3c;
      border-left: 4px solid #7e00ff;
      border-right: 4px solid #7e00ff;
      height: 700px;
      overflow: auto;

    }
    .b-white{
      max-height: 700px;
      overflow: auto;
      ul{
        padding: 0;
        max-height: 100%;
      }
      p{
        color: #494949;
        margin: 0;
      }
      p:nth-child(2n){
        background-color: #f6f6f6;
        padding: 15px 0;
        border-top: 4px solid #e6e6e6;
        border-bottom: 4px solid #e6e6e6;
      }
      li{
        justify-content: center;
        align-items: center;
        padding: 15px 0;
        color: #7e00ff;
      }
      li:nth-child(2n){
        background-color: #f6f6f6;
      } 
    }
  }
  .side-bar__hidden{
    transform: translateX(-110%);
    transition: 100ms;
  }
  .footer{
    background-color: #7e00ff;
    z-index: 99;
    position: absolute;
    width: 100%;
    max-width: 1110px;
    padding: 25px 25px;
    .btn-save,.btn-back{
      padding: 5px 10px;
      width: 120px;
      border: 3px solid #fff;
      font-size: 24px;
      i{
        margin-right: 5px;
      }
    }
    .btn-save{
      background-color: #fff;
      color: #7e00ff;
      margin-right: 5px;
    }
    .btn-back{
      background-color: #7e00ff;
      color: white;
    }
  }
  @media (max-width: 1200px){
    .side-bar__hidden{
      transform: translateX(-120%);
      transition: 100ms;

    }
  }
  @media (max-width: 1023px){
     .side-bar{
      transform: none;
      transition: 100ms;
      position: absolute;
      z-index: 999;
      height: 100%;
      overflow: hidden;
    
  }
    
    .side-bar__hidden{
      transform: translateY(-120%);
      transition: 100ms;

    }
    .sidebar-nav{
      height: 700px;
      overflow: auto;
    }
    .b-content{
      .b-gray{
        border: none;
      }
    }
  }
</style>
