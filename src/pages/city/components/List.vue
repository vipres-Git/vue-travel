<template>
  <div class="list" ref="wrapper">
    <div>
      <div class="area">
        <div class="title border-topbottom">当前城市</div>
        <div class="button-list">
          <div class="button-wrapper">
            <div class="button">{{this.city}}</div>
          </div>
        </div>
      </div>
      <div class="area">
        <div class="title border-topbottom">热门城市</div>
        <div class="button-list">
          <div class="button-wrapper" v-for="item of hot" :key="item.id" @click="handleClick(item.name)">
            <div class="button">{{item.name}}</div>
          </div>
        </div>
      </div>
      <div class="area" v-for="(item,key) of cities" :key="key" :ref="key">
        <div class="title border-topbottom">{{key}}</div>
        <div class="item-list">
          <div
            class="item border-bottom"
            v-for="innerItem of item"
            :key="innerItem.id"
            @click="handleClick(innerItem.name)"
          >{{innerItem.name}}</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Bscroll from "better-scroll";
import {mapState,mapMutations} from 'vuex'
import { log } from 'util';
import CityVue from '../City.vue';
export default {
  name: "CityList",
  mounted() {
    this.scroll = new Bscroll(this.$refs.wrapper);
  },
  computed: {
    ...mapState(['city'])
  },
  props: {
    hot: Array,
    cities: Object,
    letter: String
  },
  data() {
    return {};
  },
  methods: {
    handleClick(arg){
      // this.$store.commit('changeCity', arg)
      this.changeCity(arg)
      this.$router.push('/')
    },
    ...mapMutations(['changeCity'])
  },
  watch: {
    letter() {
      if (this.letter) {
        const el = this.$refs[this.letter][0];
        this.scroll.scrollToElement(el);
      }
    }
  }
};
</script>

<style lang="stylus" scoped>
@import '~styles/mixins.styl';
@import '~styles/varibles.styl';

.border-topbottom {
  &:before {
    border-color: #ccc;
  }

  &:after {
    border-color: #ccc;
  }
}

.border-bottom {
  &:before {
    border-color: #ccc;
  }
}

.list {
  overflow: hidden;
  position: absolute;
  top: 1.58rem;
  left: 0;
  right: 0;
  bottom: 0;

  .title {
    line-height: 0.54rem;
    background: #eee;
    padding-left: 0.2rem;
    color: #666;
    font-size: 0.26rem;
  }

  .button-list {
    padding: 0.1rem 0.6rem 0.1rem 0.1rem;
    overflow: hidden;

    .button-wrapper {
      float: left;
      width: 33.33%;

      .button {
        margin: 0.1rem;
        padding: 0.1rem 0;
        text-align: center;
        border: 0.02rem solid #ccc;
        border-radius: 0.06rem;
      }
    }
  }

  .item-list {
    padding: 0.1rem 0.6rem 0.1rem 0.1rem;

    .item {
      line-height: 0.54rem;
      padding: 0.02rem;
    }
  }
}
</style>