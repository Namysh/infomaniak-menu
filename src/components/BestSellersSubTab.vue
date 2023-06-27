<script setup>
import ProductSubTabWrapper from './ProductSubTabWrapper.vue';

const products = [
    {
        title: 'kDrive',
        description: 'Stockez, collaborez et partagez vos fichiers',
    },
    {
        title: 'Nom de domaine',
        description: 'Réservez votre nom de domaine en quelques clics',
    },
    {
        title: "VPS Cloud",
        description: 'Créez un serveur Windows ou Linux'
    },
    {
        title: 'kMail',
        description: 'Créez vos adresse mails avec votre domaine'
    },
    {
        title: 'Hébergement Web',
        description: 'Créez vos sites Internet (Wordpress + 100 CMS)'
    },
    {
        title: 'Public Cloud (IaaS)',
        description: 'Infrastructure Cloud Haute Performance'
    }
]

</script>

<template>
    <ProductSubTabWrapper>
        <div class="flex flex-col gap-6">
            <span class="text-[#333333]">Nos produits phares du moment</span>
            <div class="grid grid-cols-3">
                <div v-for="product in products" class="flex flex-col gap-2.5 p-4">
                    <span class="font-bold">{{ product.title }}</span>
                    <span class="text-[#666666]">{{ product.description }}</span>

                </div>
            </div>
        </div>
    </ProductSubTabWrapper>
</template>

<style scoped>
</style>
