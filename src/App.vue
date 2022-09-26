<script setup> 
import _ from 'lodash'
import CatsTab from './components/CatsTab.vue'
import {onMounted } from 'vue'

     const cats = [
        {
          "Nom": "Pitchoune",
          "Sexe": "Femelle",
          "Date": "2019-10-01",
          "Race": "Gouttière",
          "Prix": "1100,60",
          "Commentaires": "Aime le calme du foyer, sort peu.  Ne va jamais chasser. N'aime pas les croquettes mais ne mange que des patées. Attention à ne pas laisser près des enfants."
        },
        {
          "Nom": "Yamcha",
          "Sexe": "Mâle",
          "Date": "2016-01-26",
          "Race": "Balinois",
          "Prix": "800,00",
          "Commentaires": "Jolie robe couleur sable,miaule beaucoup"
        },
        {
          "Nom": "Poukie",
          "Sexe": "Femelle",
          "Date": "2015-09-16",
          "Race": "Chartreux",
          "Prix": "150,60",
          "Commentaires": "N'aime pas ses congénères"
        },
        {
          "Nom": "Plume",
          "Sexe": "Femelle",
          "Date": "2019-10-01",
          "Race": "Maine Coon",
          "Prix": "1500,00",
          "Commentaires": "Espiègle et joueuse"
        },
        {
          "Nom": "Zizou",
          "Sexe": "Mâle",
          "Date": "2019-01-30",
          "Race": "Européen",
          "Prix": "10,00",
          "Commentaires": "SOS animal malade"
        },
        {
          "Nom": "Séréna",
          "Sexe": "Femelle",
          "Date": "2017-04-01",
          "Race": "Ecaille de tortue",
          "Prix": "100,00",
          "Commentaires": "Chatte timide et réservée"
        },
        {
          "Nom": "Pitchin",
          "Sexe": "Femelle",
          "Date": "2019-10-01",
          "Race": "Gouttière",
          "Prix": "1100,60",
          "Commentaires": "Aime le calme du foyer, sort peu"
        },
        {
          "Nom": "Yamchou",
          "Sexe": "Mâle",
          "Date": "2016-01-26",
          "Race": "Balinois",
          "Prix": "800,00",
          "Commentaires": "Jolie robe couleur sable,miaule beaucoup"
        },
        {
          "Nom": "Poukette",
          "Sexe": "Femelle",
          "Date": "2015-09-16",
          "Race": "Chartreux",
          "Prix": "100,60",
          "Commentaires": "N'aime pas ses congénères"
        },
        {
          "Nom": "Plumo",
          "Sexe": "Mâle",
          "Date": "2018-10-01",
          "Race": "Maine Coon",
          "Prix": "1500,25",
          "Commentaires": "Espiègle et joueuse"
        },
        {
          "Nom": "Zilou",
          "Sexe": "Mâle",
          "Date": "2019-11-30",
          "Race": "Européen",
          "Prix": "10,00",
          "Commentaires": "SOS animal malade"
        },
        {
          "Nom": "Vaiana",
          "Sexe": "Femelle",
          "Date": "2017-04-01",
          "Race": "Ecaille de tortue",
          "Prix": "100,00",
          "Commentaires": "Chatte timide et réservée"
        }
      ]

      onMounted(() => {
      // On ajoute un id et on transforme le prix en number pour faciliter le tri
      _.forEach(cats , function(value , key){          
          value.id = cats.indexOf(value)
          value.Prix = _.toNumber( _.replace(value.Prix , ',' ,'.'))
      }) 
      })
</script>

<template>
  <CatsTab :cats="cats"></CatsTab>
</template>

<style scoped>
</style>
