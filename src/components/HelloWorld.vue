<template>
  <div>
    <div class="picklizr__title" v-html="'PICKLIZR'"></div>
    <div class="picklizr__grid">
      <div class="grid__box arrow-top-left"></div>
      <div class="grid__box top" v-html="people[4].name"></div>
      <div class="grid__box arrow-top-right"></div>
      <div class="grid__box left" v-html="people[1].name"></div>
      <div class="grid__box center" v-html="people[0].name"></div>
      <div class="grid__box right" v-html="people[3].name"></div>
      <div class="grid__box arrow-bottom-left"></div>
      <div class="grid__box bottom" v-html="people[2].name"></div>
      <div class="grid__box arrow-bottom-right"></div>
    </div>
    <div class="button__container">
      <div class="button" v-html="'Picklize'" v-on:click="picklize"></div>
    </div>
  </div>
</template>

<script>
  /* eslint-disable indent */

  export default {
    name: 'HelloWorld',
    props: {
      msg: String
    },
    data () {
      return {
        people: [
          {
            id: 0,
            name: 'Nick',
            isEditing: 1
          },
          {
            id: 1,
            name: 'Linda',
            isEditing: 2
          },
          {
            id: 2,
            name: 'Josh',
            isEditing: 3
          },
          {
            id: 3,
            name: 'Eric',
            isEditing: 4
          },
          {
            id: 4,
            name: 'Id',
            isEditing: 1
          }
        ]
      }
    },
    methods: {
      picklize () {
        console.log('Ni')
        this.people = this.people.map(person => ({
          id: person.id,
          name: person.name,
          isEditing: this.getRandomInt(1, 5)
        }))
          .slice(1, 5)
          .sort((a, b) => a.isEditing === b.id)
      },
      getRandomInt (min, max) {
        min = Math.ceil(min)
        max = Math.floor(max)
        return Math.floor(Math.random() * (max - min)) + min
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  .picklizr {
    &__title {
      text-align: center;
      font-size: 20px;
    }
    &__grid {
      display: grid;
      grid-template: "arrow-top-left top arrow-top-right" "left center right" "arrow-bottom-left bottom arrow-bottom-right";

      .grid {
        &__box {
          border: solid 1px;
          height: 150px;
        }
      }

      .center {
        background-image: url('../assets/pickle.png');
        background-size: cover;
      }
    }
  }

  .button {
    &__container {
      display: flex;
      justify-content: center;
      width: 100%;
    }

    height: 50px;
    padding: 5px 10px;
    background-color: lightblue;
    border-radius: 6px;
  }

</style>
