<template>
  <div class="cartcontrol">
    <transition name="fadeRotate">
      <div class="cart-decrease" v-show="food.count>0" @click.stop="decreaseCart($event)">
        <span class="icon-remove_circle_outline inner"></span>
      </div>
    </transition>
    <div class="cart-count" v-show="food.count>0">
      {{ food.count }}
    </div>
    <div id="add" class="cart-add" @click.stop="addCart($event)">
      <i class="icon-add_circle"></i>
    </div>
  </div>
</template>

<script>
import Vue from 'vue'
import { mapState, mapMutations } from 'vuex'
export default {
  props: ['food'],
  data () {
    return {
      ok: true
    }
  },
  methods: {
    addCart (event) {
      if (!event._constructed) {
        return false
      }
      if (typeof this.food.count === 'undefined') {
        Vue.set(this.food, 'count', 0)
        Vue.set(this.food, 'active', true)
      }
      this.food.count++
      if (this.food.active) {
        this.vxaddCart(this.food)
        this.food.active = false
      }
    },
    decreaseCart (event) {
      if (!event._constructed) {
        return false
      }
      this.food.count--
      if (this.food.count === 0) {
        this.vxdecreaseCart(this.food)
        this.food.active = true
      }
    },
    ...mapMutations([
      'vxaddCart',
      'vxdecreaseCart'
    ])
  },
  computed: {
    ...mapState([
      'vxselectFoods'
    ])
  }
}
</script>

<style lang="css">
</style>
