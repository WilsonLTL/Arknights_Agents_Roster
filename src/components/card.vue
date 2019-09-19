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

    <v-card-actions>
      <v-btn icon @click="show = !show">
        <v-icon>{{ show ? 'keyboard_arrow_up' : 'keyboard_arrow_down' }}</v-icon>
      </v-btn>
    </v-card-actions>

    <v-expand-transition>
      <div v-show="show">
        <div  v-if="skills.length > 0">
          <span class="headline" style="margin: 20px">幹員技能</span>
          <v-divider></v-divider>
          <v-col v-for="(item, i) in skills" :key="i">
            <v-card outlined>
              <v-list-item three-line>
                <v-list-item-avatar size="62" tile>
                  <v-img :src="item.skill_img"></v-img>
                </v-list-item-avatar>
                <v-list-item-content class="align-self-start">
                  <div>
                  <span v-for="label in item.skill_label" :key=label>
                    <v-chip x-small>{{label}}</v-chip>
                  </span>
                  </div>
                  <v-list-item-subtitle class="overline" v-text="'消耗:'+item.skill_cost"></v-list-item-subtitle>
                  <v-list-item-text class="overline" v-text="item.skill_name"></v-list-item-text>
                  <v-list-item-text style="color: #BDBDBD;" class="overline" v-text="item.skill_desc"></v-list-item-text>
                </v-list-item-content>
              </v-list-item>
            </v-card>
          </v-col>
        </div>
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
    check_list: Array,
    skills: Array
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