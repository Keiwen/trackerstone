<template>
    <div>
        <div class="container-fluid deckList">
            <div class="col-xs-4 col-sm-3 deckFiltered" v-for="(deck, id) in own" @click="pickDeck(id)">
                <deck-show-simple :deck="deck"></deck-show-simple>
            </div>
        </div>

        <hr/>
        <div class="col-xs-6">
        </div>
        <div class="col-xs-6">
            <a @click="goToManageDeck">Manage decks</a>
        </div>

    </div>
</template>


<script>
  import { mapGetters } from 'vuex'
  import DeckShowSimple from './DeckShowSimple'

  export default {
    components: {DeckShowSimple},
    computed: {
      ...mapGetters(['generateDeckTitle', 'own'])
    },
    methods: {
      pickDeck (key) {
        this.$emit('pick-deck', key)
      },
      goToManageDeck () {
        // do not use direct router link. We are in a modal,
        // it will consider that we are still in a modal
        // => scroll locked
        this.$emit('goTo', 'deckList')
      }
    }
  }
</script>

<style lang="scss" scoped>

    .deckList {
        margin-bottom: 20px;
        height: 180px;
        overflow-y: scroll;
    }

    .deckFiltered {
        height: 50px;
        border: 1px solid transparent;
        cursor: pointer;
        &:hover {
            border: 1px solid var(--orange-ts);
        }
        display: inline-block;
        line-height: 1.5;
        vertical-align: middle;
    }



</style>
