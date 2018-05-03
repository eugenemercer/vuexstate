<template>
  <div class="hello">
    <div class="left">
      <h1>{{ title }}</h1>
      <div class="ui form ">
        <div class="field">
          <form @submit.prevent="addLink">
             <input type="text" class="link-input" placeholder="Add a link" v-model="newLink"/>
         </form>
        </div>
        </div>
    
    <ul>
      <li v-for="(link, index) in links" v-bind:key="index">
        {{ link }}
        {{ countLinks }}
        <button v-on:click="removeLink(index)" class="rm ui button ">Remove</button>
      </li>
    </ul>

    </div>
    <div class="right">
        <stats />
    </div>
  </div>
</template>

<script>
import Stats from '@/components/Stats.vue'
import { mapState, mapMutations, mapActions } from 'vuex'
export default {
  name: 'HelloWorld',
    data() {
      return {
        newLink: ''
      }
    },
    components: {
      Stats
    },
    computed: {
      ...mapState([
        'title',
        'links'
      ]),
    },

      methods: {
        ...mapMutations([
          'ADD_LINK'
        ]),
        ...mapActions([
            'removeLink'
      ]),

        addLink: function() {
          this.ADD_LINK(this.newLink)
          this.newLink = '' // empty when
        },
        removeLinks: function(link) {
          //shoudlnt be plural
            this.removeLink(link)
        }
      }, // -- methods --

      getters: {
        countLinks: state => {
          return state.links.length
        }
      }
  }
</script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
