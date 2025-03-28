<template>
  <AdminLayout>
    <PageBreadcrumb />
    <div class="space-y-5 sm:space-y-6">
        <PaginatedTable
          :columns="columns"
          :items="items"
          :loading="loading"
          textEmpty="Nenhum Pedido Encontrado"
        >
          <template v-slot:cell-platform="{ item: { logo, name } }">
            <div class="flex gap-3 items-center">
              <div class="w-10 h-10 overflow-hidden rounded-full ring-3 ring-brand-500/5 flex flex-center">
                <img :src="logo" :alt="`${name} logo`" />
              </div>
              <span class="block font-medium text-gray-800 text-theme-sm dark:text-white/90">
                {{ name }}
              </span>
            </div>
          </template>
          <template v-slot:cell-action="{ item: platform }">
            <Button size="sm" @click="handleGenerateURL(platform)">Gerar Link de autorização</Button>
          </template>
          <template v-slot:cell-link="{ item }">
            <Button v-if="item" size="sm" @click="handleLink(item)">Acessar link</Button>
          </template>
        </PaginatedTable>
    </div>
  </AdminLayout>
</template>

<script lang="ts" setup>
import { computed, ref } from "vue";
import { storeToRefs } from "pinia";
import PageBreadcrumb from "@/components/common/PageBreadcrumb.vue";
import AdminLayout from "@/components/layout/AdminLayout.vue";
import Button from "@/components/ui/Button.vue";
import PaginatedTable from "@/components/tables/PaginatedTable.vue";
import type { Column } from "@/components/tables/types";
import { useAuthStore } from "@/store/auth";

const authStore = useAuthStore()
const { loading } = storeToRefs(authStore)

const columns: Column[] = [
  { key: 'platform', label: 'Plataforma' },
  { key: 'action', label: 'Ação' },
  { key: 'link', label: 'Link' },
];

const mercadolivreLink = ref('');
const shopeeLink = ref('');

const items = computed(() => {
  return [
    {
      platform: {
        logo: '/images/platform/mercado-livre.svg',
        name: 'Mercado Livre',
      },
      action: 'mercado-livre',
      link: mercadolivreLink.value,
    },
    {
      platform: {
        logo: '/images/platform/shopee.svg',
        name: 'Shopee',
      },
      action: 'shopee',
      link: shopeeLink.value,
    },
  ]
});

const handleGenerateURL = async (platform: string) => {
  if (platform === 'mercado-livre') {
    const url = await authStore.getMercadoLivreAuthorizationLink();
    mercadolivreLink.value = url.authorization_url;
  } else if (platform === 'shopee') {
    const url = await authStore.getShopeeAuthorizationLink();
    shopeeLink.value = url.authorization_url;
  }
};

const handleLink = (item: string) => {
  window.open(item, '_blank');
};
</script>
