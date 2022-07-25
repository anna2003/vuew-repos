<template>
  <div class="card card-w70">
    <div v-if="items.length">
      <component
        v-for="item in items"
        :key="item.id"
        :is="'app-' + item.type"
        v-bind="{ [item.type]: item.value }"
      ></component>
    </div>

    <h3 v-else>Добавьте первый блок, чтобы увидеть результат</h3>
  </div>
</template>

<script>
import AppTitle from "./items/AppTitle.vue";
import AppSubTitle from "./items/AppSubTitle.vue";
import AppAvatar from "./items/AppAvatar.vue";
import AppText from "./items/AppText.vue";

export default {
  props: {
    items: {
      type: Array,
    },
  },
  components: {
    AppTitle,
    "app-subtitle": AppSubTitle,
    AppAvatar,
    AppText,
  },
};
</script>