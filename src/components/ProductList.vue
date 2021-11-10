<template>
  <v-card>
    <v-card-title>Inventory</v-card-title>
    <v-card-text>
      <v-data-table
        :headers="headers"
        :items="filteredProducts"
        item-key="name"
        :search="search"
        hide-default-footer
      >
        <template v-slot:top>
          <v-text-field
            v-model="search"
            outlined
            dense
            append-icon="mdi-magnify"
            label="Search"
          ></v-text-field>
        </template>
        <template v-slot:item.quantity="{ item }">
          <v-text-field
            v-model="item.quantity"
            type="number"
            outlined
            dense
            hide-details
            placeholder="Quantity"
          >
          </v-text-field>
        </template>
        <template v-slot:item.product="{ item }">
          <span class="success--text font-weight-bold">{{ item.product }}</span>
        </template>
      </v-data-table>
    </v-card-text>
  </v-card>
</template>

<script>
import { mapState } from 'vuex'
export default {
  name: 'ProductList',
  data() {
    return {
      search: '',
      headers: [
        {
          text: 'Item code',
          value: 'code'
        },{
          text: 'Product',
          value: 'product'
        },{
          text: 'Package',
          value: 'package'
        },{
          text: 'Available units',
          value: 'units'
        },{
          text: 'Category',
          value: 'category'
        },{
          text: 'Last updated',
          value: 'lastUpdated'
        },{
          text: 'Edit available quantity',
          value: 'quantity'
        }
      ]
    }
  },
  computed: {
    ...mapState('products', ['products']),
    filteredProducts() {
      return this.products.filter((product) => {
        const upperSearch = this.search.toUpperCase()

        return product.code.toUpperCase().includes(upperSearch) ||
          product.product.toUpperCase().includes(upperSearch) ||
          product.category.toUpperCase().includes(upperSearch)
      })
    }
  }
}
</script>