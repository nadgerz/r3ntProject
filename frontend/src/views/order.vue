<script>
// import InvoiceCard from '@/components/invoice-card.vue'
import { mapActions, mapState } from 'vuex'

export default {
  name: 'user-orders',
  data() {
    return {
      orders: [],
      invoices: [],
      sInvoice: false,
      rev: '',
      product: {},
    }
  },
  async created() {
   
    this.orders = await this.fetchUserOrders(this.user._id)
    this.invoices = await this.fetchUserInvoices(this.user._id)
  },
  computed: {
    ...mapState(['user'])
  },
  methods: {
    ...mapActions(['addReview', 'fetchUserOrders', 'fetchUserInvoices']),
    async submitRev(prod){
      this.product= prod
      console.log(this.review)
      await this.addReview({
        product: this.product,
        user : this.user,
        review: this.rev,
      })
      this.$router.push(`/products/${this.product._id}`).catch(() => {})
      // location.reload()
    },
    userInput(event){
      this.rev = event.target.value
    }
}
}
</script>

<template lang="pug">
  .container.all
    .row
      .col-12.orders(v-for="order in orders" :key="order_id")
        h3.order-text Order created for "{{ order.product.name }}". Order ID : {{order._id}}
        textarea.txtarea(type="text" v-on:input="userInput($event)" placeholder="Enter your review")
        button.button(@click="submitRev(order.product)") Submit Review
        button
          router-link(:to="`/order/invoice/${order.invoice._id}`") Show Invoice
</template>
<style scoped>
* {
  margin: 10px;
  padding: 10px;
  box-sizing: border-box;
}
.all{
  display: block;
}
.orders{
  display: flex;
  padding: 5px 5px;
  color: rgb(98, 127, 139);
  font-size: 15px;
  font-weight: 100;
  background-color: rgba(248, 245, 245, 0.25);
  border-radius: 16px;
  margin: 15px 15px;
  box-shadow: 3px 3px rgba(0.1, 0.1, 0.1, 0.1);
}

</style>
