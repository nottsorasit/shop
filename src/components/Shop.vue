<template>
  <div class="container">
    <nav class="navbar"><h1 >ร้านขายผลไม้(บูด555)</h1></nav>
    <h2 align="left">รายการสินค้า</h2>
    <hr />
    <div class="row">
      <div class="col-md-2" v-for="item in products" :key="item">
        <div class="card h-100">
          <img :src="item.img" class="card-img-top" />
          <div class="card-body">
            <h4 class="card-title">{{ item.name }}</h4>
            <p class="card-text">ราคา {{ item.price }} บาท</p>
          </div>
          <div class="card-footer">
            <button class="btn btn-primary" @click="addCart(item)">
              หยิบลงตะกร้า
            </button>
          </div>
        </div>
      </div>

      <div class="col-md-12" v-if="carts != 0">
        <br />
        <h2 align="center">
          ตะกร้าสินค้า<i class="fa fa-shopping-cart" aria-hidden="true"></i>({{totalQty()}})
        </h2>
        <h3 align="right">ยอดชำระเงิน {{ total() }}บาท</h3>
        <hr />
        <table class="table">
          <thead class="thead-dark">
            <tr>
              <th scope="col">ภาพสินค้า</th>
              <th scope="col">ชื่อ</th>
              <th scope="col">ราคา</th>
              <th scope="col">จำนวน</th>
              <th scope="col">ยอดรวม</th>
              <th scope="col">ลบ</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="product in carts" :key="product">
              <td><img :src="product.img" width="50px" height="50px" /></td>
              <td>{{ product.name }}</td>
              <td>{{ product.price }}</td>
              <td>
                <i class="fa fa-minus qty-minus" @click="minusQty(product)"></i>
                {{ product.qty }}
                <i class="fa fa-plus qty-plus" @click="plusQty(product)"></i>
              </td>
              <td>{{ product.total }}</td>
              <td>
                <button
                  @click="removeProduct(product)"
                  class="btn-danger"
                >
                  <i class="fa fa-times"></i>
                </button>
              </td>
            </tr>
          </tbody>
        </table>
        <hr />
        <h3>
          <div>
            <b-button v-b-modal.modal-1>ยืนยันการสั่งซื้อ</b-button>
            <b-modal id="modal-1" title="ขอโทษครับ!">
              <p class="my-4">มันบูดแล้วครับ5555!!</p>
            </b-modal>
          </div>
        </h3>
        <h6 align="center">
          <button class="btn-danger" @click="clean()">ยกเลิกการสั่งซื้อ</button>
        </h6>
        <div></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Shop",
  data() {
    return {
      carts: [],
      num1: 0,
      num2: 0,
      num3: 0,
      num4: 0,
      num5: 0,
      num6: 0,
      products: [
        {
          id: 1,
          name: "แอปเปิล",
          price: 15,
          img:
            "https://img.freepik.com/free-photo/red-apple-with-green-leaf-isolated-white_80510-518.jpg?size=338&ext=jpg&ga=GA1.2.1347944333.1613553879",
        },
        {
          id: 2,
          name: "กล้วย",
          price: 20,
          img:
            "https://img.freepik.com/free-photo/bananas-white-background_1187-1671.jpg?size=338&ext=jpg&ga=GA1.2.1347944333.1613553879",
        },
        {
          id: 3,
          name: "องุ่น",
          price: 30,
          img:
            "https://img.freepik.com/free-photo/green-red-grape-isolated-white_1232-1957.jpg?size=626&ext=jpg&ga=GA1.2.1347944333.1613553879",
        },
        {
          id: 4,
          name: "มะม่วง",
          price: 10,
          img:
            "https://img.freepik.com/free-photo/freshness-food-life-fruit-yellow_1203-5467.jpg?size=626&ext=jpg&ga=GA1.2.1347944333.1613553879",
        },
        {
          id: 5,
          name: "ส้ม",
          price: 35,
          img:
            "https://img.freepik.com/free-photo/orange-white-white_144627-16571.jpg?size=626&ext=jpg&ga=GA1.2.1347944333.1613553879",
        },
        {
          id: 6,
          name: "มังคุด",
          price: 40,
          img:
            "https://img.freepik.com/free-photo/mangosteens-queen-fruits-ripe-mangosteen-fruit-isolated-white-background_1205-1708.jpg?size=626&ext=jpg&ga=GA1.2.1347944333.1613553879",
        },
      ],
    };
  },
  methods: {
    addCart: function (item) {
      if (item.id == 1) {
        this.num1 += 1;
        if (this.num1 <= 1) {
          this.pushData(item);
        } else {
          var found = this.findIndex(item);
          this.carts[found].qty += 1;
          this.carts[found].total =
            this.carts[found].qty * this.carts[found].price;
        }
      }
      if (item.id == 2) {
        this.num2 += 1;
        if (this.num2 <= 1) {
          this.pushData(item);
        } else {
          var found1 = this.findIndex(item);
          this.carts[found1].qty += 1;
          this.carts[found1].total =
            this.carts[found1].qty * this.carts[found1].price;
        }
      }
      if (item.id == 3) {
        this.num3 += 1;
        if (this.num3 <= 1) {
          this.pushData(item);
        } else {
          var found2 = this.findIndex(item);
          this.carts[found2].qty += 1;
          this.carts[found2].total =
            this.carts[found2].qty * this.carts[found2].price;
        }
      }
      if (item.id == 4) {
        this.num4 += 1;
        if (this.num4 <= 1) {
          this.pushData(item);
        } else {
          var found3 = this.findIndex(item);
          this.carts[found3].qty += 1;
          this.carts[found3].total =
            this.carts[found3].qty * this.carts[found3].price;
        }
      }
      if (item.id == 5) {
        this.num5 += 1;
        if (this.num5 <= 1) {
          this.pushData(item);
        } else {
          var found4 = this.findIndex(item);
          this.carts[found4].qty += 1;
          this.carts[found4].total =
            this.carts[found4].qty * this.carts[found4].price;
        }
      }
      if (item.id == 6) {
        this.num6 += 1;
        if (this.num6 <= 1) {
          this.pushData(item);
        } else {
          var found5 = this.findIndex(item);
          this.carts[found5].qty += 1;
          this.carts[found5].total =
            this.carts[found5].qty * this.carts[found5].price;
        }
      }
    },
    pushData(item) {
      this.carts.push({
        id: item.id,
        name: item.name,
        price: item.price,
        img: item.img,
        qty: 1,
        total: item.price,
      });
    },
    findIndex: function (item) {
      for (var i = 0; i < this.carts.length; i++) {
        if (this.carts[i].id == item.id) {
          return i;
        }
      }
      return -1;
    },
    minusQty: function (product) {
      product.qty -= 1;
      if (product.qty <= 1) {
        product.qty = 1;
      }
      product.total = product.price * product.qty;
    },
    plusQty: function (product) {
      product.qty += 1;
      product.total = product.price * product.qty;
    },
    removeProduct(product) {
      if (confirm("คุณต้องการลบหรือไม่ ?")) {
        var index = this.carts.indexOf(product);
        this.carts.splice(index, 1);
        if (product.id == 1) {
          this.num1 == 0;
        }
        if (product.id == 2) {
          this.num2 == 0;
        }
        if (product.id == 3) {
          this.num3 == 0;
        }
        if (product.id == 4) {
          this.num4 == 0;
        }
        if (product.id == 5) {
          this.num5 == 0;
        }
        if (product.id == 6) {
          this.num6 == 0;
        }
      }
    },
    total: function () {
      var sum = 0;
      this.carts.forEach(function (item) {
        sum += item.total;
      });
      return sum;
    },
    clean() {
      this.carts = [];
    },
    totalQty: function () {
      var d = 0;
      this.carts.forEach(function (item) {
        d += item.qty;
      });
      return d;
    },
  },
};
</script>

<style scoped>
.qty-minus {
  cursor: pointer;
  margin-right: 20px;
}
.qty-plus {
  cursor: pointer;
  margin-left: 20px;
}
.navbar{
  background: rgb(105, 177, 224);
  color: rgb(223, 235, 236);
}
</style>