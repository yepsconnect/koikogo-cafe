<script setup lang="ts">
useSeoMeta({
  title: "Кафе имени Койкого",
  description:
    "Мы рады приветствовать вас в кафе в историческом центре города - на всеми известной улице в кой-каком парке.",
  ogTitle: "Кафе имени Койкого",
  ogDescription:
    "Мы рады приветствовать вас в кафе в историческом центре города - на всеми известной улице в кой-каком парке.",
  ogImage: "https://koikogo.cafe/logo.png",
  ogUrl: "https://koikogo.cafe/",
  twitterTitle: "Кафе имени Койкого",
  twitterDescription:
    "Мы рады приветствовать вас в кафе в историческом центре города - на всеми известной улице в кой-каком парке.",
  twitterImage: "https://koikogo.cafe/logo.png",
  twitterCard: "summary",
});

useHead({
  link: [
    {
      rel: "icon",
      type: "image/png",
      href: "logo.png",
    },
  ],
});

// composables
const { menu, menuAlco } = useMenu();
const { order } = useOrder();

// state
const categories = [
  "завтраки до 13:00",
  "закуски",
  "салаты",
  "супы",
  "основные блюда",
  "пицца",
  "паста",
  "гарниры",
  "десерты",
  "кофе",
  "чай",
  "фирменный чай",
  "напитки",
  "лимонады",
  "морсы",
  "милкшейки",
];

const alcoCategories = [
  "коктейли (безалкогольные)",
  "белые вина",
  "красные вина",
  "розовые вина",
  "игристые вина",
  "вина по бокалам",
  "пиво",
  "коктейли",
];
</script>

<template>
  <div>
    <div class="h-screen w-full flex justify-center items-center">
      <div class="flex flex-col md:flex-row items-center md:items-end">
        <Logo class="max-w-64" animated />
        <h1 class="text-4xl font-bold uppercase">
          <span class="text-2xl">Кафе</span>
          <br />
          Имени
          <br />
          Койкого
        </h1>
      </div>
    </div>
    <div class="mb-12">
      <div id="menu" class="py-6">
        <h2 class="text-4xl text-center">Меню</h2>
      </div>
      <div class="flex flex-col gap-12 mt-6">
        <div v-for="(category, index) in categories" :key="index">
          <h3 class="text-3xl uppercase">{{ category }}</h3>
          <div class="flex flex-col gap-2 mt-3">
            <template v-for="(item, index) in menu" :key="index">
              <DishItem v-if="item.category === category" :dish="item" />
            </template>
          </div>
        </div>
      </div>
    </div>
    <div>
      <div class="py-6">
        <h2 class="text-4xl text-center">Винная карта бара</h2>
      </div>
      <div class="flex flex-col gap-12 mt-6">
        <div v-for="(category, index) in alcoCategories" :key="index">
          <h3 class="text-3xl uppercase">{{ category }}</h3>
          <div class="flex flex-col gap-2 mt-3">
            <template v-for="(item, index) in menuAlco" :key="index">
              <DishItem v-if="item.category === category" :dish="item" />
            </template>
          </div>
        </div>
      </div>
    </div>
    <div
      v-if="order.length"
      class="sticky flex justify-between bottom-0 bg-white py-5 border-t mt-10"
    >
      <p>Выбрано блюд: {{ order.length }}</p>
      <NuxtLink :to="{ name: 'order' }" class="active:underline">
        Посмотреть
      </NuxtLink>
    </div>
  </div>
</template>