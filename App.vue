<template>
  <ScrollView>
    <view class="bar"></view>
    <view class="canvas">
      <image
        resizeMode="cover"
        :style="{height: 100}"
        :source="{uri: 'https://www-konga-com-res.cloudinary.com/w_auto,f_auto,fl_lossy,dpr_auto,q_auto/media/catalog/product/S/O/145816_1545587421.jpg'}"
      ></image>
    </view>
    <view class="container">
      <!-- form - input contact -->
      <view class="form-wrapper">
        <text>Add New Member</text>
        <text-input
            underlineColorAndroid='transparent'
            placeholder="Enter new member"
            :style="{height: 40, width: 250, borderWidth: 1, borderColor: '#cecece', borderRadius: 3, paddingLeft: 10, paddingRight: 10, marginBottom: 5}"
            v-model="memberName"
          />
        <touchable-opacity :on-press="onTapSubmit">
          <text class="btn-primary sm-radius .white-text">Enter</text>
        </touchable-opacity>
      </view>

      <!-- display contacts -->
      <view class="wrapper gap-up-10">
        <view class="flex header-tilt">
          <text :style="{color: '#33b27b', fontWeight: '600'}">MEMBER LIST</text>
        </view>

        <view class="contact-wrapper" >
          <view v-if="loading" class="loader-wrapper">
            <image :source="loader" class="loader" />
          </view>

          <view v-else v-for="(contact, key) in contactList" :key="key">
            <view class="contact-list card">
              <!-- //top -->
              <view class="flex">
                <view>
                  <image
                  class="img-wrapper"
                  :source="{uri: 'https://www-konga-com-res.cloudinary.com/w_auto,f_auto,fl_lossy,dpr_auto,q_auto/media/catalog/product/S/O/145816_1545587421.jpg'}"
                ></image>
                </view>
                <view class="top-wrap">
                  <text class="sub" :style="{color: 'rgba(33, 33, 33, 0.9)', fontWeight: '600', fontSize: 15}">{{ contact.email }}</text>
                  <view class="flex">
                    <text class="title" :style="{fontWeight: '300'}">Medium: </text>
                    <text class="title" :style="{color: '#33b27b', fontWeight: '300'}">{{ contact.invitation_medium }}</text>
                  </view>
                </view>
              </view>

              <!-- //details -->
              <view>
                <text class="title grey-text">{{ contact.address }}</text>
              </view>

              <!-- //footer -->
              <view class="flex" :style="{ marginTop: 10, justifyContent: 'flex-end'}">
                <text class="ctn-edit">Edit</text>
              </view>
            </view>
          </view>
        </view>
      </view>
    </view>
  </ScrollView>
</template>

<script>
import axios from 'axios'
import loader from './assets/loader.gif'

const AUTH_TOKEN = `BearereyJhbGciOiJIUzI1NiJ9.eyJ1c2VyIjoyfQ.Qtxy5mDBDF4y_s8TlWPTHAiEKPvI1crqhZM1zjfg7Ys`;
axios.defaults.baseURL = 'https://qontactsky.herokuapp.com/';
axios.defaults.headers.post['Content-Type'] = 'application/x-www-form-urlencoded';
axios.defaults.headers.common['http_authorization'] = AUTH_TOKEN;

export default {
  data() {
    return {
      memberName: null,
      contactList: [],
      loading: true,
      loader: loader
    };
  },
  methods: {
    onTapSubmit() {
      axios.post(`contact`, {
        email: this.memberName
        }).then(result => {
          console.log("result ",result);
      }).catch(error => {
        console.log("failed ", error);
      }).finally();
      this.memberName = '';
    },
    loadContacts() {
      axios.get(`contact`).then(result => {
        this.contactList = result.data.contacts;
        this.loading = false;
      }).catch(error => {
        console.log("failed ", error);
      }).finally()
    }
  },
  mounted() {
    this.loadContacts();
  }
};
</script>
 
<style>
.container {
  background-color: #f5f5f5;
  align-items: center;
  justify-content: center;
  flex: 1;
  padding: 10;
}
.text-color-primary {
  color: red;
}
.white-text {
  color: #ffffff;
}
.btn-primary {
  background-color: #33b27b;
  padding-left: 20;
  padding-right: 20;
  padding-top: 10;
  padding-bottom: 10;
  text-align: center;
}
.sm-radius {
  border-radius: 2;
}
.name {
  color: white;
  font-size: 100;
}
.center {
  text-align: center;
}
.form-wrapper {
  margin-top: 10;
  margin-bottom: 10;
}
.wrapper {
  width: 100%;
  height: 100%;
  flex: 1;
}
.img-wrapper {
  width: 40;
  height: 40;
  border-radius: 35;
}
.gap-up-10 {
  margin-top: 25;
}
.contact-wrapper {
  width: 100%;
  height: 100%;
}
.loader-wrapper {
  flex-direction: row;
  justify-content: center;
  padding: 10;
}
.contact-list {
  padding-top: 10;
  padding-bottom: 10;
  margin-top: 10;
}
.grey-text {
  color: rgba(111, 111, 111, 0.995);
  font-size: 13;
}
.card {
  border-radius: 5;
  border-width: 1;
  border-color: rgba(210, 210, 210, 0.6);
  background-color: #ffffff;
  padding: 10;
}
.card .title {
  font-weight: 400;
  font-size: 30;
}
.card .title {
  font-weight: 200;
  font-size: 20;
}
.flex {
  display: flex;
  flex-direction: row;
  flex: 1;
}
.flex .first {
  text-align: left;
  flex: 1;
}
.flex .others {
  text-align: left;
  flex: 2;
}
.bar {
  width: 100%;
  background-color: #33b27b;
  padding: 10;
}
.loader {
  width: 100;
  height: 100;
}
.header-tilt {
  background-color: #f5f5f5;
  border-color: #a4c2b5;
  justify-content: center;
  border-width: 1;
  padding: 10;
}
.top-wrap {
  padding-left: 10;
}
.top-wrap .title {
  color: rgb(33, 33, 33);
  font-size: 70;
}
.ctn-edit {
  border-color: #a4c2b5;
  color: #a4c2b5;
  border-width: 1;
  padding: 8;
  text-align: center;
  min-width: 120;
}
.canvas {
  width: 100%;
  height: 100;
}
</style>
