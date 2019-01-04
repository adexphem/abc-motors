<template>
  <ScrollView>
    <view class="bar"></view>
    <view class="container">
      <image
        :style="{width: 200, height: 200}"
        :source="{uri: 'https://www-konga-com-res.cloudinary.com/w_auto,f_auto,fl_lossy,dpr_auto,q_auto/media/catalog/product/S/O/145816_1545587421.jpg'}"
      ></image>
      
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

      <view class="flex-container header">
        <text class="white-text first">Medium</text>
        <text class="white-text others">Email Address</text>
      </view>

      <scroll-view class="contact-wrapper" >
        <view v-for="(contact, key) in contactList" :key="key">
          <view class="flex-container contact-list">
            <text class="first">{{ contact.invitation_medium }}</text>
            <text class="others">{{ contact.email }}</text>
          </view>
        </view>
      </scroll-view>
    </view>
  </ScrollView>
  
</template>

<script>
import axios from 'axios'

const AUTH_TOKEN = `BearereyJhbGciOiJIUzI1NiJ9.eyJ1c2VyIjoyfQ.Qtxy5mDBDF4y_s8TlWPTHAiEKPvI1crqhZM1zjfg7Ys`;
axios.defaults.baseURL = 'https://qontactsky.herokuapp.com/';
axios.defaults.headers.post['Content-Type'] = 'application/x-www-form-urlencoded';
axios.defaults.headers.common['http_authorization'] = AUTH_TOKEN;

export default {
  data() {
    return {
      memberName: null,
      contactList: []
    };
  },
  methods: {
    onTapSubmit() {
      this.contactList = '';
    }
  },
  mounted() {
    axios.get(`contact`).then(result => {
      this.contactList = result.data.contacts;
    }).catch(error => {
      console.log("failed ", error);
    }).finally()
  }
};
</script>
 
<style>
.container {
  background-color: #ffffff;
  align-items: center;
  justify-content: center;
  flex: 1;
  padding: 20;
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
.header {
  width: 98%;
  background-color: rgb(2, 38, 26);
  padding-top: 10;
  padding-bottom: 10;
}
.form-wrapper {
  margin-top: 10;
  margin-bottom: 10;
}
.contact-wrapper {
  width: 98%;
  height: 100;
}
.contact-list {
  padding-top: 10;
  padding-bottom: 10;
  border-color: rgba(97, 97, 97, 0.2);
  border-bottom-width: 1;
}
.flex-container {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
}
.flex-container .first {
  text-align: left;
  flex: 1;
}
.flex-container .others {
  text-align: left;
  flex: 2;
}
.bar {
  width: 100%;
  background-color: #33b27b;
  padding: 10;
}
</style>
