<template>
  <div>
    <b-collapse
        aria-id="contentIdForA11y2"
        class="panel is-finish"
        animation="slide"
        :open.sync="isOpen">
      <div
          slot="trigger"
          class="panel-heading"
          role="button"
          aria-controls="contentIdForA11y2">
        <div class="level">
          <div class="level-left">
            Select Your Colour Service
          </div>
          <div v-if="selectedMensColour.id" class="level-right">
            {{ selectedMensColour.service }}: {{ selectedMensColourPrice | toCurrency }}
          </div>
        </div>
      </div>
      <div class="section columns is-multiline is-mobile">
        <div v-for="(service, i) in mensColourPrices"
             :key="i" class="column">
          <div class="button is-small is-finish is-outlined"
               :class="{ 'activeSelectedFinish': i === activeItem}"
               @click="$store.commit('UPDATE_SELECTED_MENS_COLOUR', service); isOpen = false; selectItem(i)"
               v-text="service.service"
          />
        </div>
      </div>
    </b-collapse>
  </div>
</template>
<script>
import { mapState, mapGetters } from 'vuex'

export default {
  data() {
    return {
      isOpen: true,
      activeItem: null
    }
  },

  methods: {
    selectItem(i) {
      this.activeItem = i
    },
  },

  computed: {
    ...mapState(['selectedMensColour', 'levels', 'level']),
    ...mapGetters(['mensColourPrices', 'selectedMensColourPrice'])
  }
}
</script>