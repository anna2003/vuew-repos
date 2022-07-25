<template>
  <p v-if="comments.length === 0">
    <button class="btn primary" @click="$emit('load-comments')">
      Загрузить комментарии
    </button>
  </p>
  <div class="card" v-else>
    <h2>Комментарии</h2>
    <ul class="list">
      <li class="list-item" v-for="item in comments" :key="item.id">
        <div>
          <p>
            <strong>{{ item.email }}</strong>
          </p>
          <small>{{ item.body }}</small>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    comments: {
      type: Array,
    },
  },
  emits: ["load-comments"],
};
</script>