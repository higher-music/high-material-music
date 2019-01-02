<template>
  <div class="song-list-container">
    <div v-for="(item,index) in data" :key="index" class="song-list-wapper" @click="playIndex(index)">
      <div class="song-list">
        <div v-if="showRank" class="rank">{{ index+1 }}</div>
        <img
          v-if="showAlbum"
          :src="item.image"
          :alt="item.name"
          :title="item.name">
        <div class="track-info">
          <div class="song-name-container">
            <span>{{ item.name }}</span>
          </div>
          <div class="secondary-info">
            <span>{{ item.singer }}</span>
          </div>
        </div>
        <v-menu bottom left>
          <v-btn slot="activator" dark icon>
            <v-icon>more_vert</v-icon>
          </v-btn>

          <v-list>
            <v-list-tile
              v-for="(item, i) in items"
              :key="i">
              <v-list-tile-title>{{ item.title }}</v-list-tile-title>
            </v-list-tile>
          </v-list>
        </v-menu>
      </div>
    </div>
  </div>
</template>

<script>
import { mapActions } from 'vuex'
export default {
  name: 'SongList',
  props: {
    showRank: {
      type: Boolean,
      default: false
    },
    showAlbum: {
      type: Boolean,
      default: true
    },
    innerData: {
      type: Boolean,
      default: false
    },
    data: {
      type: Array,
      default: () => {
        return []
      }
    }
  },
  data(){
    return {
      items: [
        { title: 'Play Next' },
        { title: 'Play Later' }
      ]
    }
  },
  methods: {
    ...mapActions([
      'addSongToCurrentIndex'
    ]),
    playIndex(index) {
      this.addSongToCurrentIndex(this.data[index])
    }
  }
}
</script>

<style lang="scss" scoped>
  .song-list-container{
    padding-left: 20px;
    padding-right: 20px;
    .song-list-wapper {
      display: flex;
      height: 60px;
      border-radius: 5px;
      cursor: pointer;
      .song-list{
        overflow: hidden;
        display: flex;
        flex: 1;
        align-items: center;
        .rank{
          text-align: center;
          width: 20px;
          padding-left: 10px;
          font-weight: 600;
        }
        img{
          height: 40px;
          width: 40px;
          margin-right: 10px;
          border-radius: 2px;
          box-shadow: 0 0 10px rgba(0,0,0,.5);
          margin-left: 10px;
        }
        .track-info{
          white-space: nowrap;
          overflow: hidden;
          text-overflow: ellipsis;
          flex: 1;
          display: flex;
          flex-direction: column;
          .song-name-container{
            display: flex;
            align-items: center;
          }
          .secondary-info{
            display: flex;
            color: #b3b3b3;
            font-size: 14px;
          }
        }
      }
    }
    .song-list-wapper:hover{
      background-color: rgba(255,255,255,.04);
    }
  }
</style>