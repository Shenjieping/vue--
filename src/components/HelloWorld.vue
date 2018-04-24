<template>
  <div class="pageContainer">
    <div>当前第{{currentPage}}页</div>
    <ul class="pagesInner">
      <li class="page" @click="prevOrNext(-1)"><span class="fa fa-chevron-left" aria-hidden="true">&#139;</span></li>
      <li class="page"
          v-for="(item, index) in pages" 
          :key="index"
          @click="select(item)"
          :class="{actived: item === currentPage}">
        <span>{{item}}</span>
      </li>
      <li class="page" @click="prevOrNext(1)"><span class="fa fa-chevron-right" aria-hidden="true">&#155;</span></li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      currentPage: 1,
      totalPages: 50
    }
  },
  computed: {
    pages() {
      const c = this.currentPage
      const t = this.totalPages
      console.log('===>>', this.currentPage)
      if (c <= 5) {
        return [1, 2, 3, 4, 5, 6, 7, 8, 9, '...', t]  //第一种情况
      } else if (c >= t - 4) {
        return [1, '...', t-8, t-7, t-6, t-5, t-4, t-3, t-2, t-1, t] //第二种情况
      } else {
        return [1, '...', c-3, c-2, c-1, c, c+1, c+2, c+3, '...', t]  //第三种情况
      }
    }
  },
  methods: {
    select(n) {
        if (n === this.currentPage) return 
        if (typeof n === 'string') return 
        this.currentPage = n;
    },
    prevOrNext(n) {
      this.currentPage += n
      this.currentPage < 1
      ? this.currentPage = 1
      : this.currentPage > this.totalPages
        ? this.currentPage = this.totalPages
        : null
    }
  }
};
</script>

<style lang="less">
  * {
    margin: 0;
    padding: 0;
  }
  ul, ol, li {
    list-style: none;
  }
  .pagesInner {
    height: 35px;
    margin-top: 20px;
    .page {
      float: left;
      margin-left: 10px;
      height: 35px;
      width: 35px;
      line-height: 35px;
      text-align: center;
      border: 1px solid #999;
      border-radius: 3px;
      cursor: pointer;
      -webkit-user-select: none;
      .fa {
        font-size: 24px;
      }
    }
  }
  .actived {
      border-color: #2d8cf0;
      background-color: #2d8cf0;
      color: #fff;
  }
</style>