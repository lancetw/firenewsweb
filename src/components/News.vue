<template>
  <div class="ui text four item menu">
    <div class="ui item toggle checkbox">
      <input type="checkbox" id="checkbox0" v-model="showAll">
      <label for="checkbox0">顯示所有新聞</label>
    </div>
    <div class="ui item toggle checkbox">
      <input type="checkbox" id="checkbox1" v-model="showBg">
      <label for="checkbox1">顯示背景圖</label>
    </div>
  </div>

  <div v-show="!showBg">
    <div class="ui horizontal divider header">近期本局相關新聞</div>

    <div class="ui segment fixed">
      <div id="news">
        <div v-if="loading5" class="ui active inverted dimmer">
          <div class="ui large loader"></div>
        </div>
        <span v-if="!loading5 && items8.length == 0">今日無相關新聞</span>
        <ol>
          <li v-if="!showAll&&item.status" v-bind:class="{'focus': item.status}" v-for="item in items8 | orderBy 'time'">
            <a v-bind:class="{'focus': item.status}" v-if="!hideTextLink" v-bind:class="{ 'hide-link-underline': hideLinkUnderline }" href="{{ item.originLink }}" target="_blank">{{ item.title }}</a><span v-if="hideTextLink">{{ item.title }}</span>（{{ item.source }}）<span v-if="!hideTime">{{ item.timeText }}&nbsp;</span>
            <a v-bind:class="{'focus': item.status}" class="shortlink" v-if="!hideShortUrl" v-bind:class="{ 'hide-link-underline': hideLinkUnderline }"href="{{ item.link }}" target="_blank">{{ item.link }}</a>
          </li>
          <li v-if="showAll" v-bind:class="{'focus': item.status}" v-for="item in items8 | orderBy 'time'">
            <a v-bind:class="{'focus': item.status}" v-if="!hideTextLink" v-bind:class="{ 'hide-link-underline': hideLinkUnderline }" href="{{ item.originLink }}" target="_blank">{{ item.title }}</a><span v-if="hideTextLink">{{ item.title }}</span>（{{ item.source }}）<span v-if="!hideTime">{{ item.timeText }}&nbsp;</span>
            <a v-bind:class="{'focus': item.status}" class="shortlink" v-if="!hideShortUrl" v-bind:class="{ 'hide-link-underline': hideLinkUnderline }"href="{{ item.link }}" target="_blank">{{ item.link }}</a>
          </li>
        </ol>
      </div>
    </div>

    <div class="ui horizontal divider header">今天的消防新聞</div>

    <div class="ui segment fixed">
      <div id="news">
        <div v-if="loading" class="ui active inverted dimmer">
          <div class="ui large loader"></div>
        </div>
        <p v-if="!loading">{{ today }} 消防新聞</p>
        <span v-if="!loading && items1.length == 0">待搜集</span>
        <ol>
          <li v-if="!showAll&&item.status" v-bind:class="{'focus': item.status}" v-bind:item="item" v-for="item in items1 | orderBy 'time'">
            <a v-bind:class="{'focus': item.status}" v-if="!hideTextLink" v-bind:class="{ 'hide-link-underline': hideLinkUnderline }" href="{{ item.originLink }}" target="_blank">{{ item.title }}</a><span v-if="hideTextLink">{{ item.title }}</span>（{{ item.source }}）<span v-if="!hideTime">{{ item.timeText }}&nbsp;</span>
            <a v-bind:class="{'focus': item.status}" class="shortlink" v-if="!hideShortUrl" v-bind:class="{ 'hide-link-underline': hideLinkUnderline }" href="{{ item.link }}" target="_blank">{{ item.link }}</a>
          </li>
          <li v-if="showAll" v-bind:class="{'focus': item.status}" v-bind:item="item" v-for="item in items1 | orderBy 'time'">
            <a v-bind:class="{'focus': item.status}" v-if="!hideTextLink" v-bind:class="{ 'hide-link-underline': hideLinkUnderline }" href="{{ item.originLink }}" target="_blank">{{ item.title }}</a><span v-if="hideTextLink">{{ item.title }}</span>（{{ item.source }}）<span v-if="!hideTime">{{ item.timeText }}&nbsp;</span>
            <a v-bind:class="{'focus': item.status}" class="shortlink" v-if="!hideShortUrl" v-bind:class="{ 'hide-link-underline': hideLinkUnderline }" href="{{ item.link }}" target="_blank">{{ item.link }}</a>
          </li>
        <br />
        <p v-if="!loading">{{ today }} 消防新聞（續）</p>
          <li v-if="!showAll&&item.status" v-bind:class="{'focus': item.status}" v-for="item in items2 | orderBy 'time'">
            <a v-bind:class="{'focus': item.status}" v-if="!hideTextLink" v-bind:class="{ 'hide-link-underline': hideLinkUnderline }" href="{{ item.originLink }}" target="_blank">{{ item.title }}</a><span v-if="hideTextLink">{{ item.title }}</span>（{{ item.source }}）<span v-if="!hideTime">{{ item.timeText }}&nbsp;</span>
            <a v-bind:class="{'focus': item.status}" class="shortlink" v-if="!hideShortUrl" v-bind:class="{ 'hide-link-underline': hideLinkUnderline }"href="{{ item.link }}" target="_blank">{{ item.link }}</a>
          </li>
          <li v-if="showAll" v-bind:class="{'focus': item.status}" v-for="item in items2 | orderBy 'time'">
            <a v-bind:class="{'focus': item.status}" v-if="!hideTextLink" v-bind:class="{ 'hide-link-underline': hideLinkUnderline }" href="{{ item.originLink }}" target="_blank">{{ item.title }}</a><span v-if="hideTextLink">{{ item.title }}</span>（{{ item.source }}）<span v-if="!hideTime">{{ item.timeText }}&nbsp;</span>
            <a v-bind:class="{'focus': item.status}" class="shortlink" v-if="!hideShortUrl" v-bind:class="{ 'hide-link-underline': hideLinkUnderline }"href="{{ item.link }}" target="_blank">{{ item.link }}</a>
          </li>
        </ol>
      </div>
    </div>

    <div class="ui horizontal divider header">明天的消防新聞</div>

    <div class="ui segment fixed">
      <div id="news">
        <div v-if="loading" class="ui active inverted dimmer">
          <div class="ui large loader"></div>
        </div>
        <p v-if="!loading">{{ nextday }} 消防新聞</p>
        <span v-if="!loading && items3.length == 0">待搜集</span>
        <ol>
          <li v-if="!showAll&&item.status" v-bind:class="{'focus': item.status}" v-for="item in items3 | orderBy 'time'">
            <a v-bind:class="{'focus': item.status}" v-if="!hideTextLink" v-bind:class="{ 'hide-link-underline': hideLinkUnderline }" href="{{ item.originLink }}" target="_blank">{{ item.title }}</a><span v-if="hideTextLink">{{ item.title }}</span>（{{ item.source }}）<span v-if="!hideTime">{{ item.timeText }}&nbsp;</span>
            <a v-bind:class="{'focus': item.status}" class="shortlink" v-if="!hideShortUrl" v-bind:class="{ 'hide-link-underline': hideLinkUnderline }" href="{{ item.link }}" target="_blank">{{ item.link }}</a>
          </li>
          <li v-if="showAll" v-bind:class="{'focus': item.status}" v-for="item in items3 | orderBy 'time'">
            <a v-bind:class="{'focus': item.status}" v-if="!hideTextLink" v-bind:class="{ 'hide-link-underline': hideLinkUnderline }" href="{{ item.originLink }}" target="_blank">{{ item.title }}</a><span v-if="hideTextLink">{{ item.title }}</span>（{{ item.source }}）<span v-if="!hideTime">{{ item.timeText }}&nbsp;</span>
            <a v-bind:class="{'focus': item.status}" class="shortlink" v-if="!hideShortUrl" v-bind:class="{ 'hide-link-underline': hideLinkUnderline }" href="{{ item.link }}" target="_blank">{{ item.link }}</a>
          </li>
          <br />
          <p v-if="!loading">{{ nextday }} 消防新聞（續）</p>
          <li v-if="!showAll&&item.status" v-bind:class="{'focus': item.status}" v-for="item in items4 | orderBy 'time'">
            <a v-bind:class="{'focus': item.status}" v-if="!hideTextLink" v-bind:class="{ 'hide-link-underline': hideLinkUnderline }" href="{{ item.originLink }}" target="_blank">{{ item.title }}</a><span v-if="hideTextLink">{{ item.title }}</span>（{{ item.source }}）<span v-if="!hideTime">{{ item.timeText }}&nbsp;</span>
            <a v-bind:class="{'focus': item.status}" class="shortlink" v-if="!hideShortUrl" v-bind:class="{ 'hide-link-underline': hideLinkUnderline }"href="{{ item.link }}" target="_blank">{{ item.link }}</a>
          </li>
          <li v-if="showAll" v-bind:class="{'focus': item.status}" v-for="item in items4 | orderBy 'time'">
            <a v-bind:class="{'focus': item.status}" v-if="!hideTextLink" v-bind:class="{ 'hide-link-underline': hideLinkUnderline }" href="{{ item.originLink }}" target="_blank">{{ item.title }}</a><span v-if="hideTextLink">{{ item.title }}</span>（{{ item.source }}）<span v-if="!hideTime">{{ item.timeText }}&nbsp;</span>
            <a v-bind:class="{'focus': item.status}" class="shortlink" v-if="!hideShortUrl" v-bind:class="{ 'hide-link-underline': hideLinkUnderline }"href="{{ item.link }}" target="_blank">{{ item.link }}</a>
          </li>
        </ol>
      </div>
    </div>

    <div class="ui horizontal divider header">今日新竹市相關新聞</div>

    <div class="ui segment fixed">
      <div id="news">
        <div v-if="loading2" class="ui active inverted dimmer">
          <div class="ui large loader"></div>
        </div>
        <span v-if="!loading2 && items5.length == 0">今日無相關新聞</span>
        <ol>
          <li v-if="!showAll&&item.status" v-bind:class="{'focus': item.status}" v-for="item in items5 | orderBy 'time'">
            <a v-bind:class="{'focus': item.status}" v-if="!hideTextLink" v-bind:class="{ 'hide-link-underline': hideLinkUnderline }" href="{{ item.originLink }}" target="_blank">{{ item.title }}</a><span v-if="hideTextLink">{{ item.title }}</span>（{{ item.source }}）<span v-if="!hideTime">{{ item.timeText }}&nbsp;</span>
            <a v-bind:class="{'focus': item.status}" class="shortlink" v-if="!hideShortUrl" v-bind:class="{ 'hide-link-underline': hideLinkUnderline }"href="{{ item.link }}" target="_blank">{{ item.link }}</a>
          </li>
          <li v-if="showAll" v-bind:class="{'focus': item.status}" v-for="item in items5 | orderBy 'time'">
            <a v-bind:class="{'focus': item.status}" v-if="!hideTextLink" v-bind:class="{ 'hide-link-underline': hideLinkUnderline }" href="{{ item.originLink }}" target="_blank">{{ item.title }}</a><span v-if="hideTextLink">{{ item.title }}</span>（{{ item.source }}）<span v-if="!hideTime">{{ item.timeText }}&nbsp;</span>
            <a v-bind:class="{'focus': item.status}" class="shortlink" v-if="!hideShortUrl" v-bind:class="{ 'hide-link-underline': hideLinkUnderline }"href="{{ item.link }}" target="_blank">{{ item.link }}</a>
          </li>
        </ol>
      </div>
    </div>

    <div class="ui horizontal divider header">今日低氣壓（颱風）相關新聞</div>

    <div class="ui segment fixed">
      <div id="news">
        <div v-if="loading3" class="ui active inverted dimmer">
          <div class="ui large loader"></div>
        </div>
        <span v-if="!loading3 && items6.length == 0">今日無相關新聞</span>
        <ol>
          <li v-if="!showAll&&item.status" v-bind:class="{'focus': item.status}" v-for="item in items6 | orderBy 'time'">
            <a v-bind:class="{'focus': item.status}" v-if="!hideTextLink" v-bind:class="{ 'hide-link-underline': hideLinkUnderline }" href="{{ item.originLink }}" target="_blank">{{ item.title }}</a><span v-if="hideTextLink">{{ item.title }}</span>（{{ item.source }}）<span v-if="!hideTime">{{ item.timeText }}&nbsp;</span>
            <a v-bind:class="{'focus': item.status}" class="shortlink" v-if="!hideShortUrl" v-bind:class="{ 'hide-link-underline': hideLinkUnderline }"href="{{ item.link }}" target="_blank">{{ item.link }}</a>
          </li>
          <li v-if="showAll" v-bind:class="{'focus': item.status}" v-for="item in items6 | orderBy 'time'">
            <a v-bind:class="{'focus': item.status}" v-if="!hideTextLink" v-bind:class="{ 'hide-link-underline': hideLinkUnderline }" href="{{ item.originLink }}" target="_blank">{{ item.title }}</a><span v-if="hideTextLink">{{ item.title }}</span>（{{ item.source }}）<span v-if="!hideTime">{{ item.timeText }}&nbsp;</span>
            <a v-bind:class="{'focus': item.status}" class="shortlink" v-if="!hideShortUrl" v-bind:class="{ 'hide-link-underline': hideLinkUnderline }"href="{{ item.link }}" target="_blank">{{ item.link }}</a>
          </li>
        </ol>
      </div>
    </div>

    <div class="ui horizontal divider header">今日地震相關新聞</div>

    <div class="ui segment fixed">
      <div id="news">
        <div v-if="loading4" class="ui active inverted dimmer">
          <div class="ui large loader"></div>
        </div>
        <span v-if="!loading4 && items7.length == 0">今日無相關新聞</span>
        <ol>
          <li v-if="!showAll&&item.status" v-bind:class="{'focus': item.status}" v-for="item in items7 | orderBy 'time'">
            <a v-bind:class="{'focus': item.status}" v-if="!hideTextLink" v-bind:class="{ 'hide-link-underline': hideLinkUnderline }" href="{{ item.originLink }}" target="_blank">{{ item.title }}</a><span v-if="hideTextLink">{{ item.title }}</span>（{{ item.source }}）<span v-if="!hideTime">{{ item.timeText }}&nbsp;</span>
            <a v-bind:class="{'focus': item.status}" class="shortlink" v-if="!hideShortUrl" v-bind:class="{ 'hide-link-underline': hideLinkUnderline }"href="{{ item.link }}" target="_blank">{{ item.link }}</a>
          </li>
          <li v-if="showAll" v-bind:class="{'focus': item.status}" v-for="item in items7 | orderBy 'time'">
            <a v-bind:class="{'focus': item.status}" v-if="!hideTextLink" v-bind:class="{ 'hide-link-underline': hideLinkUnderline }" href="{{ item.originLink }}" target="_blank">{{ item.title }}</a><span v-if="hideTextLink">{{ item.title }}</span>（{{ item.source }}）<span v-if="!hideTime">{{ item.timeText }}&nbsp;</span>
            <a v-bind:class="{'focus': item.status}" class="shortlink" v-if="!hideShortUrl" v-bind:class="{ 'hide-link-underline': hideLinkUnderline }"href="{{ item.link }}" target="_blank">{{ item.link }}</a>
          </li>
        </ol>
      </div>
    </div>
  </div>

  <small class="ui horizontal inverted divider header">
    lancetw&lt;at&gt;gmail.com, 2016
  </small>
</template>

<script>
import moment from 'moment'
import { sortBy, pickBy, isEmpty } from 'lodash'

const serverAddress = process.env.API_SERVER

export default {
  ready () {
    this.loading = true
    this.$http.get(serverAddress + '/api/news/v1/main').then((response) => {
      const rdata = sortBy(response.data.news, (o) => { return o.time })
      const items1 = pickBy(rdata, (o) => {
        return moment(o.time).isBetween(moment().subtract(1, 'day').hour(17).minute(55), moment().hour(5).minute(55), 'minute', '[)')
      })
      if (!isEmpty(items1)) this.items1 = items1
      const items2 = pickBy(rdata, (o) => {
        return moment(o.time).isBetween(moment().hour(5).minute(55), moment().hour(17).minute(55), 'minute', '[)')
      })
      if (!isEmpty(items2)) this.items2 = items2
      const items3 = pickBy(rdata, (o) => {
        return moment(o.time).isBetween(moment().hour(17).minute(55), moment().add(1, 'day').hour(5).minute(55), 'minute', '[)')
      })
      if (!isEmpty(items3)) this.items3 = items3
      const items4 = pickBy(rdata, (o) => {
        return moment(o.time).isBetween(moment().add(1, 'day').hour(5).minute(55), moment().add(1, 'day').hour(17).minute(55), 'minute', '[)')
      })
      if (!isEmpty(items4)) this.items4 = items4

      this.loading = false
    }, (errors) => {
      console.log(errors)
    })

    this.loading2 = true
    this.$http.get(serverAddress + '/api/news/v1/city').then((response) => {
      const rdata = sortBy(response.data.news, (o) => { return o.time })
      const items5 = pickBy(rdata, (o) => {
        return moment(o.time).isBetween(moment().subtract(1, 'day').hour(17).minute(55), moment().add(1, 'day').hour(5).minute(55), 'minute', '[)')
      })
      if (!isEmpty(items5)) this.items5 = items5

      this.loading2 = false
    }, (errors) => {
      console.log(errors)
    })

    this.loading3 = true
    this.$http.get(serverAddress + '/api/news/v1/typhon').then((response) => {
      const rdata = sortBy(response.data.news, (o) => { return o.time })
      const items6 = pickBy(rdata, (o) => {
        return moment(o.time).isBetween(moment().subtract(1, 'day').hour(17).minute(55), moment().add(1, 'day').hour(5).minute(55), 'minute', '[)')
      })
      if (!isEmpty(items6)) this.items6 = items6

      this.loading3 = false
    }, (errors) => {
      console.log(errors)
    })

    this.loading4 = true
    this.$http.get(serverAddress + '/api/news/v1/earthquake').then((response) => {
      const rdata = sortBy(response.data.news, (o) => { return o.time })
      const items7 = pickBy(rdata, (o) => {
        return moment(o.time).isBetween(moment().subtract(1, 'day').hour(17).minute(55), moment().add(1, 'day').hour(5).minute(55), 'minute', '[)')
      })
      if (!isEmpty(items7)) this.items7 = items7

      this.loading4 = false
    }, (errors) => {
      console.log(errors)
    })

    this.loading5 = true
    this.$http.get(serverAddress + '/api/news/v1/hcfd').then((response) => {
      const rdata = sortBy(response.data.news, (o) => { return o.time })
      const items8 = pickBy(rdata, (o) => {
        return moment(o.time).isBetween(moment().subtract(1, 'day').hour(5).minute(55), moment().add(1, 'day').hour(5).minute(55), 'minute', '[)')
      })
      if (!isEmpty(items8)) this.items8 = items8

      this.loading5 = false
    }, (errors) => {
      console.log(errors)
    })
  },
  data () {
    return {
      focusItem: {
        focus: false
      },
      loading: false,
      loading2: false,
      loading3: false,
      loading4: false,
      loading5: false,
      hideTime: false,
      hideLinkUnderline: false,
      hideShortUrl: false,
      hideTextLink: false,
      today: moment().format('YYYY/MM/DD'),
      nextday: moment().add(1, 'day').format('YYYY/MM/DD'),
      items1: [],
      items2: [],
      items3: [],
      items4: [],
      items5: [],
      items6: [],
      items7: [],
      items8: []
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h2 {
  font-size: 1.4rem;
  font-weight: normal;
  line-height: auto;
  margin: 0;
}

#news {
  font-family: "標楷體", DFKai-SB, BiauKai, STKaiti;
  font-size: 1.4rem;
  text-align: center;
  color: #000;
}

.ui.divider.header {
  font-size: 1.2rem;
}

.ui.divider.header, .ui.item.toggle.checkbox label {
  color: rgba(251,251,251,1) !important;
  text-shadow: 0 0 2px #333;
}

#news p {
  text-align: left;
}

#news ol {
  margin: 0;
  padding: 0;
  line-height: auto;
  text-align: left;
}

#news ol li {
  color: #aaa;
  margin: 0;
  padding: 0;
  line-height: auto;
  font-weight: normal;
}

#news ol li.focus {
  color: black;
}

#news ol li a {
  margin: 0;
  padding: 0;
  color: #aaa;
  text-decoration: underline;
  font-weight: normal;
}

#news ol li a.focus {
  color: black;
}

#news ol li a.shortlink {
  display: table;
  font-weight: normal;
}

#news ol li a.shortlink.focus {
  color: blue;
}

#news ol li a.hide-link-underline {
  text-decoration: none;
}

.ui.segment.fixed {
  padding: 40px 100px;
  background: rgba(255, 255, 255, 0.8);
  border: none;
}

.ui.inverted.dimmer {
  opacity: 0.3;
}

.ui.item.toggle.checkbox label {
  font-size: 15px;
  color: #000;
}

.ui.toggle.checkbox input:checked ~ .box:before, .ui.toggle.checkbox input:checked ~ label:before {
  background-color: rgba(255, 255, 255, 0.5) !important;
}

.ui.toggle.checkbox > input:checked~label {
  color: rgba(255, 255, 255, 1) !important;
  text-shadow: 0 0 2px #999;
}

</style>
