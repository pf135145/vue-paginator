<template>
  <div class="page-cont">
    <ul>
      <li id="page-pre" class="page-item" :class="{'btn-disable': currentPage == 1}" @click="prevPage">
        <span>‹</span>
      </li>
      <li v-for="(page, index) in showArr" :key="index" class="page-item" :class="{'btn-active': page == currentPage }" @click="jump(page)">
        <span>{{page}}</span>
      </li>
      <li id="page-next" class="page-item" :class="{'btn-disable': currentPage == pageCount}" @click="nextPage">
        <span>›</span>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    conf: Object 
  },
  data: function() {
    return {
      currentPage: 1,
      totalNum: this.conf.totalCount,
      size: this.conf.size,
      showLen: this.conf.showLen,
      showArr: [],
    }
  },
  created() {
    this.init()
  },
  computed: {
    pageCount() {
      return Math.ceil(this.totalNum / this.size);
    }
  },
  methods: {
    init() {
      this.pager();
    },
    pager() {
      if (this.showLen < this.pageCount) {
        let start;
        let end;
        let len2start = this.currentPage - Math.floor(this.showLen / 2);
        let len2end = this.currentPage + Math.floor(this.showLen / 2);

        if (len2start >= 1 && len2end <= this.pageCount) {
          start = len2start;
          end = len2end;
        } else if (len2start < 1) {
          start = 1;
          end = this.showLen;
        } else if (len2end > this.pageCount){
          start = this.pageCount - this.showLen + 1;
          end = this.pageCount;
        }
        this.showArr = [];
        for (let i=start; i<=end; i++) {
          this.showArr.push(i);
        }
      }
    },
    prevPage(){
      if(this.currentPage == 1) {
        return 
      }
      this.jump(this.currentPage - 1);
    },
    nextPage() {
      if(this.currentPage == this.pageCount) {
        return 
      }
      this.jump(this.currentPage + 1);
    },
    jump(index) {
      if (this.currentPage == index) {
        return
      }
      this.currentPage = index;
      this.pager();
      this.changeFn && this.changeFn();
    },
  }
}
</script>

<style>
  #page-pre {
    margin-right: 8px;
  }
  #page-next {
    margin-left: 4px;
  }
  .page-item span{
    font-size: 14px;
    user-select:none;
  }
  .page-item {
    height: 32px;
    width: 32px;
    color: #666;
    border: 1px solid #d7dde4;
    border-radius: 4px;
    text-align: center;
    float: left;
    line-height: 30px;
    cursor: pointer;
    margin-right: 4px;
    transition: all .2s ease-in-out;
  }
  .page-item:hover {
    color: #39f;
    border-color: #39f;
  }
  .btn-active {
    background-color: #39f;
    border-color: #39f !important;
    color: #fff !important;
  }
  .btn-disable {
    cursor: not-allowed;
    color: #666 !important;
    border: 1px solid #d7dde4 !important;
  }
</style>
