<template>
  <v-card class="mx-auto" max-width="344" v-bind:style=" { boxShadow: rating_color[rating-1]} ">
    <v-list-item>
      <v-list-item-avatar color="grey">
        <v-avatar >
            <v-img :src="avatar"/>
        </v-avatar>
      </v-list-item-avatar>
      <v-list-item-content>
        <v-list-item-title class="headline">{{name}}</v-list-item-title>
        <v-list-item-subtitle>{{eName}}</v-list-item-subtitle>
      </v-list-item-content>
    </v-list-item>
    <v-img :src="img" height="300px"></v-img>
    <v-card-title>
      <span v-for="item in label" :key=item>
        <v-chip v-if="item=='當前暫不實裝'||item=='公開招募不可'" color="pink darken-1" small>{{item}}</v-chip>
        <v-chip v-else small>{{item}}</v-chip>
      </span>
      <span class="grey--text subtitle-2">{{desc}}</span>
    </v-card-title>

    <!-- <v-card-actions>
      <v-btn icon @click="show = !show">
        <v-icon>{{ show ? 'keyboard_arrow_up' : 'keyboard_arrow_down' }}</v-icon>
      </v-btn>
    </v-card-actions> -->

    <v-expand-transition>
      <div v-show="show">
        <v-card-text>{{story}}</v-card-text>
      </div>
    </v-expand-transition>
  </v-card>
</template>

<script>
import json from '../data/agents.json';

export default {
  name: "card",
  props: {
    avatar: String,
    eName: String,
    name: String,
    desc: String,
    img: String,
    label: Array ,
    story: String,
    rating: Number,
    check_list: Array
  },
  data: () => ({
    rating_color: json.rating_color,
    show: false
  })
};
</script>

<style scoped>
  .card {
    -webkit-box-shadow: 2px 5px 6px 5px rgba(255,171,0,0.4); 
    box-shadow: 2px 5px 5px 5px rgba(255,171,0,0.4);
  }
</style>