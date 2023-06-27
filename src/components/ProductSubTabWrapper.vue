<script setup>
</script>

<template>
  <div class="flex bg-white relative w-[400px] flex-col">
    <div class="p-6 bg-[rgb(242,244,246)] w-full">
      <div class="border-[rgb(231,235,238)] w-full bg-white border w-full px-2 py-4">
        <input class=" w-full outline-0 h-full" placeholder="Recherche  r un produit, un mot clé" />
      </div>
    </div>
    <div class="p-6 bg-white w-full">
      <slot />
    </div>
  </div>
</template>

<style scoped></style>
