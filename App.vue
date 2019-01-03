<template>
  <view class="container">
    <image
      :style="{width: 200, height: 200}"
      :source="{uri: 'https://www-konga-com-res.cloudinary.com/w_auto,f_auto,fl_lossy,dpr_auto,q_auto/media/catalog/product/S/O/145816_1545587421.jpg'}"
    ></image>
    <text>Shoe Name:</text>
    <text-input
        underlineColorAndroid='transparent'
        placeholder="Enter product name"
        :style="{height: 40, width: 250, borderWidth: 1, borderColor: '#cecece', borderRadius: 3, paddingLeft: 10, paddingRight: 10, marginBottom: 5}"
        v-model="productName"
      />
    <touchable-opacity :on-press="onTapSubmit">
      <text class="btn-primary sm-radius">Enter</text>
    </touchable-opacity>
    <scroll-view class="product-wrapper" >
      <view v-for="(product, key) in productListing" :key="key">
        <text class="product-list">{{ product.name }}</text>
      </view>
    </scroll-view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      childName: "Inioluwa",
      productName: null,
      productListing: [
        {
          sku: 'sjds7dj',
          name: "ABC Sneaker"
        }
      ]
    };
  },
  methods: {
    onTapSubmit() {
      this.productListing.push({
        name: this.productName,
        sku: Math.random().toString(36).substr(2, 9)
      })
      this.productName = '';
      console.log("onTapSubmit tapped ", this.productListing);
    }
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

.btn-primary {
  background-color: rgb(2, 38, 26);
  padding-left: 20;
  padding-right: 20;
  padding-top: 10;
  padding-bottom: 10;
  color: #c9c9c9;
}

.sm-radius {
  border-radius: 2;
}

.name {
  color: white;
  font-size: 100;
}

.product-wrapper {
  width: 98%;
  height: 20;
}
.product-list {
  padding-top: 10;
  padding-bottom: 10;
  border-color: rgba(97, 97, 97, 0.2);
  border-bottom-width: 1;
}
</style>
