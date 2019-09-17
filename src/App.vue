<template>
  <div id="app">
    <v-app id="inspire">
      <v-card class="overflow-hidden">
        <appBar />
        <v-sheet
          id="scrolling-techniques-6"
          class="overflow-y-auto"
          color="grey darken-4"
          max-height="1000"
        >
          <v-container style="margin-top: 60px; height: 100vh">
            <v-row>
              <v-col
                v-if="checkInList(item)"
                v-for="item in agents"
                :key="item.eName"
                sm="6"
                md="4"
                lg="3"
                xl="2"
              >
                <card
                  :key="item.name"
                  :avatar="item.avatar"
                  :name="item.name"
                  :eName="item.eName"
                  :img="item.img"
                  :label="item.label"
                  :desc="item.desc"
                  :rating="item.rating"
                  :story="item.story"
                  :skills="item.skill"
                  :check_list="check_list"
                />
              </v-col>
            </v-row>
            <welcomeCard :hidden="hidden" />
          </v-container>
          <v-speed-dial
            v-model="fab"
            :bottom="bottom"
            :right="right"
            :transition="transition"
            fixed
          >
            <template v-slot:activator>
              <v-btn v-model="fab" color="blue-grey darken-3" dark fab>
                <v-icon v-if="fab" v-on:click="close">close</v-icon>
                <v-avatar v-else>
                  <img
                    src="https://img.moegirl.org/common/1/10/%E4%BC%81%E9%B9%85%E7%89%A9%E6%B5%8102.png"
                  />
                </v-avatar>
              </v-btn>
            </template>
            <v-card min-width="350" style="margin-right: 300px;" color="blue-grey darken-3">
              <v-card-title>幹員標籤</v-card-title>
              <v-divider class="mx-4"></v-divider>
              <v-card-text v-for="items in label_list" :key="items.type">
                <v-chip color="cyan">{{items.type}}</v-chip>
                <br />
                <span v-for="item in items.list" :key="item">
                  <v-chip
                    class="seleted"
                    v-if="check_list.includes(item)"
                    color="blue darken-1"
                    v-on:click="click(item)"
                    small
                  >{{item}}</v-chip>
                  <v-chip class="seleted" v-else outlined v-on:click="click(item)" small>{{item}}</v-chip>
                </span>
              </v-card-text>
            </v-card>
          </v-speed-dial>
        </v-sheet>
      </v-card>
    </v-app>
  </div>
</template>

<script>
import appBar from "./components/appBar";
import card from "./components/card";
import welcomeCard from "./components/welcomeCard";
import json from "./data/agents.json";

export default {
  name: "App",
  components: {
    appBar,
    card,
    welcomeCard
  },
  data: () => ({
    //json data
    agents: json.agents,
    label_list: json.label_list,
    check_list: [],

    // system data
    direction: "top",
    fab: false,
    tabs: null,
    top: false,
    right: true,
    bottom: true,
    hidden: false,
    transition: "slide-y-reverse-transition"
  }),
  created() {
    this.$vuetify.theme.dark = true;
    this.agents = this.agents.sort(function(a, b) {
      return a.rating < b.rating ? 1 : -1;
    });
  },
  methods: {
    checkInList(item) {
      let status = true;
      if (this.check_list.length > 0) {
        this.check_list.forEach(ele => {
          if (!item.label.includes(ele)) status = false;
        });
        this.hidden = true;
        return status;
      } else {
        this.hidden = false;
        return false;
      }
    },
    click(item) {
      this.fab = false;
      this.transition = "none";
      if (!this.check_list.includes(item)) {
        this.check_list.push(item);
      } else {
        let index = this.check_list.indexOf(item);
        this.check_list.splice(index, 1);
      }
    },
    close() {
      this.transition = "slide-y-reverse-transition";
      this.fab = true;
    }
  }
};
</script>

<style >
.sheet {
  background: url("http://5b0988e595225.cdn.sohucs.com/images/20180929/7d0d223025cf4d53bcdd590327dd6ebe.png");
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
}
.seleted {
  background-color: #1e88e5;
}
</style>