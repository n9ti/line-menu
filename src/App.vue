<template>
  <div id="app">
    <main>
      <section>
        <header>
          <h2>LINE MENU</h2>
          <!-- <p>For a clean looking design that doesn't get in the way</p> -->
        </header>
        <aside v-if="menuForYou !== null">
          <img
            v-if="menuForYou['Photo (link or picture)']"
            alt
            :src="menuForYou['Photo (link or picture)']"
          >
          <h3>{{menuForYou.Menu}}</h3>
          <p>{{menuForYou["สาธยายความอร่อย"]}}</p>
          <h6>Recommended by {{menuForYou["Recommended by"]}}</h6>
          <p v-if="menuForYou['Self-cook / Order'] === 'Order'">
            <a :href="menuForYou.Location" target="_blank">
              <em>
                ไปที่ร้าน
                ↗
              </em>
            </a>
          </p>
        </aside>
        <header>
          <button v-if="menuForYou !== null" @click="randomMenu">ลองใหม่อีกที ยังไม่ถูกใจ !</button>
          <button v-else @click="randomMenu">ไม่รู้จะกินอะไรดี กดเลย !</button>
        </header>
        <aside v-for="(menu, index) in menus" :key="index">
          <img v-if="menu['Photo (link or picture)']" alt :src="menu['Photo (link or picture)']">
          <h3>{{menu.Menu}}</h3>
          <p>{{menu["สาธยายความอร่อย"]}}</p>
          <h6>Recommended by {{menu["Recommended by"]}}</h6>
          <p v-if="menu['Self-cook / Order'] === 'Order'">
            <a :href="menu.Location" target="_blank">
              <em>
                ไปที่ร้าน
                ↗
              </em>
            </a>
          </p>
        </aside>
      </section>
    </main>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      menusData: [],
      menuForYou: null
    };
  },
  computed: {
    menus() {
      return this.menusData.filter(menu => {
        return menu.Menu !== null;
      });
    }
  },
  methods: {
    randomMenu() {
      this.menuForYou = this.menus[
        Math.floor(Math.random() * this.menus.length)
      ];
    }
  },
  mounted() {
    fetch("https://sheet.best/api/sheets/6c57c02a-6898-4da4-9a1a-197edd2ea063")
      .then(response => {
        return response.json();
      })
      .then(data => {
        this.menusData = data;
      });
  }
};
</script>

<style>
</style>
