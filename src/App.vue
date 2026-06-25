<script setup>
import { computed, reactive, ref } from "vue";
import heroImage from "../assets/restaurant-hero.png";

const navLinks = [
  { href: "#menu", label: "菜单" },
  { href: "#experience", label: "体验" },
  { href: "#reserve", label: "预订" },
];

const features = [
  {
    number: "01",
    title: "顺着季节做饭",
    text: "菜单随产地和时令调整，也保留几道熟客常常想念的味道。",
  },
  {
    number: "02",
    title: "看得见的烟火气",
    text: "炭火、煎台与甜品台都在视线之内，香气会先一步来到桌边。",
  },
  {
    number: "03",
    title: "照顾每一种相聚",
    text: "半杯餐酒、无酒精饮品和儿童友好选择，让每一桌都吃得自在。",
  },
];

const dishes = [
  {
    type: "前菜",
    title: "炙烤甜虾与青柠泡沫",
    text: "甜虾经炭火轻轻炙热，配上青柠香气，清爽得像晚风。",
    price: "¥68",
  },
  {
    type: "主菜",
    title: "炭烤和牛小排",
    text: "外层微焦、肉汁丰盈，配绵密土豆泥和黑蒜汁，是今晚很踏实的一道主菜。",
    price: "¥198",
    featured: true,
  },
  {
    type: "甜品",
    title: "桂花梨塔",
    text: "酥皮托住慢煮香梨，桂花奶油带来轻柔香气，适合两个人分着吃。",
    price: "¥58",
  },
];

const restaurantInfo = [
  { label: "地址", value: "梧桐路 19 号 1 层" },
  { label: "电话", value: "021-8800-1926" },
  { label: "人均", value: "¥260 - ¥420" },
];

const guestOptions = ["2 位", "3-4 位", "5-6 位", "7 位以上"];
const timeOptions = ["18:00", "18:30", "19:00", "19:30", "20:00"];

const reservation = reactive({
  name: "",
  guests: guestOptions[0],
  date: "",
  time: timeOptions[0],
});

const reserveForm = ref(null);
const note = ref("");

const minDate = computed(() => new Date().toISOString().slice(0, 10));

function submitReservation() {
  if (!reserveForm.value?.checkValidity()) {
    reserveForm.value?.reportValidity();
    return;
  }

  const name = reservation.name.trim() || "您";
  note.value = `${name}，已收到 ${reservation.date} ${reservation.time} 的预订信息，我们会尽快与您确认。`;
}
</script>

<template>
  <header class="site-header">
    <a class="brand" href="#top" aria-label="雾屿餐厅首页">
      <span class="brand-mark">W</span>
      <span>雾屿餐厅</span>
    </a>
    <nav class="nav-links" aria-label="主导航">
      <a v-for="link in navLinks" :key="link.href" :href="link.href">{{ link.label }}</a>
    </nav>
    <a class="header-action" href="#reserve">预约座位</a>
  </header>

  <main id="top">
    <section class="hero" aria-label="雾屿餐厅首屏">
      <img class="hero-image" :src="heroImage" alt="温暖灯光下的现代餐厅与精致菜品" />
      <div class="hero-shade"></div>
      <div class="hero-content">
        <p class="eyebrow">Seasonal Dining · Open Kitchen</p>
        <h1>灯光刚刚亮起，<span>今晚一起慢慢吃饭。</span></h1>
        <p class="hero-copy">
          雾屿餐厅想留给你一段不赶时间的晚餐。热汤、炭火、刚出炉的面包和一杯顺口的酒，都为桌边的人慢慢准备好。
        </p>
        <div class="hero-actions">
          <a class="button primary" href="#reserve">立即预订</a>
          <a class="button secondary" href="#menu">看看今晚菜单</a>
        </div>
      </div>
    </section>

    <section class="intro-section" id="experience">
      <div class="section-kicker">Dining Experience</div>
      <div class="intro-grid">
        <h2>像回到熟悉的餐桌，也像赴一场小小的约定。</h2>
        <p>
          我们用当季蔬果、慢炖汤汁和开放厨房的烟火气，准备一顿轻松但有记忆点的饭。空间安静温暖，服务不打扰，却会在你需要时及时出现。
        </p>
      </div>
      <div class="feature-row" aria-label="餐厅特色">
        <div v-for="feature in features" :key="feature.number">
          <span>{{ feature.number }}</span>
          <strong>{{ feature.title }}</strong>
          <p>{{ feature.text }}</p>
        </div>
      </div>
    </section>

    <section class="menu-section" id="menu">
      <div class="section-heading">
        <div>
          <div class="section-kicker">Chef's Picks</div>
          <h2>今晚推荐</h2>
        </div>
        <a href="#reserve">预订时可备注忌口、生日或纪念日</a>
      </div>
      <div class="menu-grid">
        <article
          v-for="dish in dishes"
          :key="dish.title"
          class="dish-card"
          :class="{ featured: dish.featured }"
        >
          <p class="dish-type">{{ dish.type }}</p>
          <h3>{{ dish.title }}</h3>
          <p>{{ dish.text }}</p>
          <span>{{ dish.price }}</span>
        </article>
      </div>
    </section>

    <section class="reserve-section" id="reserve">
      <div class="reserve-copy">
        <div class="section-kicker">Reserve</div>
        <h2>把今晚的位置，先为你留好。</h2>
        <p>
          晚餐时段 17:30 - 22:30。周末建议提前 2 天预订，6 人以上可安排半开放包间；如果是生日、纪念日或带家人来，我们也会尽量多准备一点小心意。
        </p>
        <dl class="info-list">
          <div v-for="item in restaurantInfo" :key="item.label">
            <dt>{{ item.label }}</dt>
            <dd>{{ item.value }}</dd>
          </div>
        </dl>
      </div>
      <form ref="reserveForm" class="reserve-form" @submit.prevent="submitReservation">
        <label>
          姓名
          <input v-model="reservation.name" type="text" name="name" placeholder="您的称呼" required />
        </label>
        <label>
          人数
          <select v-model="reservation.guests" name="guests">
            <option v-for="option in guestOptions" :key="option">{{ option }}</option>
          </select>
        </label>
        <label>
          日期
          <input v-model="reservation.date" type="date" name="date" :min="minDate" required />
        </label>
        <label>
          时间
          <select v-model="reservation.time" name="time">
            <option v-for="option in timeOptions" :key="option">{{ option }}</option>
          </select>
        </label>
        <button type="submit">提交预订</button>
        <p class="form-note" role="status" aria-live="polite">{{ note }}</p>
      </form>
    </section>
  </main>

  <footer class="site-footer">
    <span>雾屿餐厅 Wuyu Dining</span>
    <span>周二至周日 11:30 - 14:00 / 17:30 - 22:30</span>
  </footer>
</template>
