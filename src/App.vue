<script>
import Layout from "./components/Layout.vue";
import Header from "./components/Header.vue";
import Footer from "./components/Footer.vue";
import Catalog from "./components/Catalog.vue";
import UiPopup from "./ui/UiPopup.vue";

const MOCK_DATA = [
  {
    id: 0,
    title: "«Рождение Венеры» Сандро Боттичелли",
    description: "Lorem ipsum dolor sit amet consectetur adipisicing elit. Quisquam, quia.",
    images: ["assets/image0.jpg", "assets/image1.jpg", "assets/image2.jpg", "assets/image3.jpg"],
    price: 1000000,
    oldPrice: 2000000,
    sold: false,
  },
  {
    id: 1,
    title: "«Тайная вечеря»  Леонардо да Винчи",
    description: "Lorem ipsum dolor sit amet consectetur adipisicing elit. Quisquam, quia.",
    images: ["assets/image1.jpg", "assets/image2.jpg", "assets/image3.jpg", "assets/image0.jpg"],    
    price: 3000000,
    sold: false,
  },
  {
    id: 2,
    title: "«Сотворение Адама» Микеланджело",
    description: "Lorem ipsum dolor sit amet consectetur adipisicing elit. Quisquam, quia.",
    images: ["assets/image2.jpg", "assets/image3.jpg", "assets/image0.jpg", "assets/image1.jpg"],    
    price: 5000000,
    oldPrice: 6000000,
    sold: false,
  },
  {
    id: 3,
    title: "«Урок анатомии»  Рембрандт",
    description: "Lorem ipsum dolor sit amet consectetur adipisicing elit. Quisquam, quia.",
    images: ["assets/image3.jpg", "assets/image0.jpg", "assets/image1.jpg", "assets/image2.jpg"],    
    price: 1000000,
    oldPrice: 2000000,
    sold: true,
  },
];

export default {
  components: {
    Layout,
    Header,
    Footer,
    Catalog,
    UiPopup
  },

  data() {
    return {
      list: MOCK_DATA,
      cart: [1],
      search: ''
    };
  },

  computed: {
    filteredList() {
      return this.search ? this.list.filter(item => item.title.toLowerCase().includes(this.search.toLowerCase())) : this.list;
    }
  },

  created() {
    this.cart = JSON.parse(localStorage.getItem('cart')) || [];
  },

  methods: {
    handleAddToCart(id) {
      console.log('qwe', id);
      this.cart.push(id);
    },

    handleRemoveFromCart(id) {
      console.log('qwe', id);
      this.cart = this.cart.filter(item => item !== id);
    },
    handleSearch(value) {
      this.search = value;
    }
  },

  watch: {
    cart() {
      localStorage.setItem('cart', JSON.stringify(this.cart));
    }
  },

};
</script>

<template>
  <Layout>
    <template #header>
      <Header @search="handleSearch" />
    </template>
    <template #main>
      <Catalog 
        title="Картины эпохи Возрождения" 
        :items="filteredList"
        :cart="cart"
        @addToCart="handleAddToCart"
        @removeFromCart="handleRemoveFromCart"
      />
    </template>
    <template #footer>
      <Footer />
    </template>
  </Layout>
</template>

