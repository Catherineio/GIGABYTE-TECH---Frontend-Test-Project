<template>
  <q-item
    clickable
    :class="[{ active: active }, 'nav-link']"
    @click="$emit('click')"
    tag="a"
    :href="link"
  >
    <q-item-section>
      <q-item-label>{{ title }}</q-item-label>
    </q-item-section>
  </q-item>
</template>

<script setup>
defineProps({
  title: String,
  link: String,
  active: Boolean,
})
</script>

<style scoped>
.nav-link {
  background: transparent;
  transition:
    background 0.2s,
    font-weight 0.2s;
}
.nav-link:hover {
  background: #90ee90;
  font-weight: bold;
}
.active {
  background: #90ee90;
  font-weight: bold;
  color: #222;
  border-left: 6px solid #fff;
}
.q-item__label {
  font-size: 1.1rem;
}
</style>
