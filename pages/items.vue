<template>
    <BreezeAuthenticatedLayout>
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Homebrew Items
            </h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-white overflow-hidden shadow-sm sm:rounded-lg">
                    <div class="p-6 bg-white border-b border-gray-200">
                      <v-data-table
                        :headers="headers"
                        :items="items"
                        :items-per-page="5"
                        class="elevation-1"
                      />
                    </div>
                </div>
            </div>
        </div>
    </BreezeAuthenticatedLayout>
</template>

<script>
import BreezeAuthenticatedLayout from '@/layouts/authenticated.vue'

export default {
  head: {
    title: 'Items',
  },

  middleware: 'authenticated',

  components: {
    BreezeAuthenticatedLayout,
  },

  data() {
    return {
      items: [],
      headers: [
        { text: 'Name', value: 'name' },
        { text: 'Price', value: 'price.asString' },
      ],
    };
  },

  methods: {
    getItems() {
      this.$axios.get('/api/items/').then(({ data }) => {
        this.items = data.data;
      });
    },
  },

  mounted() {
    this.getItems();
  }
}
</script>