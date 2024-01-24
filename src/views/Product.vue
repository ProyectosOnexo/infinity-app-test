<template>
  <div class="wrapper">
    <div class="outer">
      <div class="content animated fadeInLeft">
        <h1>
          {{ currentProducto.product_name }}
        </h1>
        <p>
          {{ currentProducto.product_description }}
        </p>

        <div class="button">
          <a href="#">${{ currentProducto.product_price }}</a
          ><a class="cart-btn" href="#"
            ><i class="cart-icon ion-bag"></i>ADD TO CART</a
          >
        </div>
      </div>
      <img
        :src="currentProducto.product_image_url"
        width="300px"
        class="animated fadeInRight"
      />
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import products from "./../assets/data/products.json";

export default {
  name: "ProductView",
  data() {
    return {
      productos: products,
      currentProducto: {
        product_id: "",
        product_name: "",
        product_description: "",
        product_price: 0,
        product_sku: "",
        product_category: "",
        product_image_url: "",
      },
    };
  },
  mounted() {
    (function () {
      var accountGUID = "e0a4074ec4a4477e0d7d61aa359ca278";
      var tagID = "test_farolito_contact_tag";
      var config = "";

      // DO NOT EDIT BELOW THIS LINE
      for (
        var odc_requested = !1,
          scripts = document.getElementsByTagName("SCRIPT"),
          s = 0;
        s < scripts.length;
        s++
      )
        scripts[s].src &&
          /oracleinfinity.*odc\.\js/.test(scripts[s].src) &&
          (odc_requested = !0);
      if (!odc_requested) {
        var sc_scripts = document.getElementsByTagName("script")[0],
          sc = document.createElement("script");
        if (((sc.async = !0), void 0 === config)) var config = "";
        config && (config = "?_ora.config=" + config),
          (sc.src =
            "//d.oracleinfinity.io/infy/acs/account/" +
            accountGUID +
            "/js/" +
            tagID +
            "/odc.js" +
            config),
          sc_scripts.parentNode.insertBefore(sc, sc_scripts);
      }
    })();

    this.currentProducto = this.getProduct(this.$route.query.id);

    this.infinityViewProduct(
      this.currentProducto.product_id,
      this.currentProducto.product_sku
    );
  },
  methods: {
    getProduct(id) {
      let product = this.productos.find((product) => product.product_id === id);

      return product;
    },
    infinityViewProduct(id, sku) {
      // Declare Your Parameters (or leave object empty {})
      var cxDataObject = {
        "wt.tx_e": "v",
        "wt.pn_sku": sku,
        "wt.userMembership": "87780",
        "wt.userEmail": "mail.paulosan@gmail.com",
      };

      // DO NOT EDIT BELOW THIS LINE - ORA.view()
      window.ORA = window.ORA || { productReady: [] };
      ORA.productReady.push([
        "analytics",
        (function (cxDataObject) {
          return function () {
            return ORA.view({ data: cxDataObject });
          };
        })(cxDataObject),
      ]);
    },
  },
};
</script>

<style scoped>
* {
  box-sizing: border-box;
}

.wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
  font-family: Montserrat;
  width: 100%;
}

.outer {
  position: relative;
  background: #fff;
  height: 350px;
  width: 550px;
  overflow: hidden;
  display: flex;
  align-items: center;
}

img {
  position: absolute;
  top: 0px;
  right: -20px;
  z-index: 0;
  animation-delay: 0.5s;
}

.content {
  animation-delay: 0.3s;
  position: absolute;
  left: 20px;
  z-index: 3;
}

h1 {
  color: #111;
}

p {
  width: 280px;
  font-size: 13px;
  line-height: 1.4;
  color: #aaa;
  margin: 20px 0;
}

.bg {
  display: inline-block;
  color: #fff;
  background: cornflowerblue;
  padding: 5px 10px;
  border-radius: 50px;
  font-size: 0.7em;
}
.button {
  width: fit-content;
  height: fit-content;
  margin-top: 10px;
}

.button a {
  display: inline-block;
  overflow: hidden;
  position: relative;
  font-size: 11px;
  color: #111;
  text-decoration: none;
  padding: 10px 15px;
  border: 1px solid #aaa;
  font-weight: bold;
}

.button a:after {
  content: "";
  position: absolute;
  top: 0;
  right: -10px;
  width: 0%;
  background: #111;
  height: 100%;
  z-index: -1;
  transition: width 0.3s ease-in-out;
  transform: skew(-25deg);
  transform-origin: right;
}

.button a:hover:after {
  width: 150%;
  left: -10px;
  transform-origin: left;
}

.button a:hover {
  color: #fff;
  transition: all 0.5s ease;
}

.button a:nth-of-type(1) {
  border-radius: 50px 0 0 50px;
  border-right: none;
}

.button a:nth-of-type(2) {
  border-radius: 0px 50px 50px 0;
}

.cart-icon {
  padding-right: 8px;
}

.footer {
  position: absolute;
  bottom: 0;
  right: 0;
}
</style>