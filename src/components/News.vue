<template>
  <div class="ui text four item menu">
    <div class="ui item toggle checkbox">
      <input type="checkbox" id="checkbox0" v-model="showAll">
      <label for="checkbox0">全部來源</label>
    </div>
    <div class="ui item toggle checkbox">
      <input type="checkbox" id="checkbox1" v-model="showBg">
      <label for="checkbox1">切換顯示</label>
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

    <div v-show="items9.length != 0">
      <div class="ui horizontal divider header">近期 Facebook 公開群組輿情</div>
      <div class="ui raised segment fixed">
        <div id="fb">
          <ul>
            <li v-for="item in items9 | orderBy 'time'">
              {{ item.timeText }} [{{ item.source }}]<a v-if="!hideTextLink" v-bind:class="{ 'hide-link-underline': hideLinkUnderline }" href="{{ item.originLink }}" target="_blank">{{ item.message.substring(0, 100) }}</a><span v-if="hideTextLink">{{ item.message }}</span>
            </li>
          </ul>
          <ul>
            <li v-for="item in items10 | orderBy 'time'">
              {{ item.timeText }} [{{ item.source }}]<a v-if="!hideTextLink" v-bind:class="{ 'hide-link-underline': hideLinkUnderline }" href="{{ item.originLink }}" target="_blank">{{ item.title.substring(0, 100) }}</a><span v-if="hideTextLink">{{ item.title }}</span>
            </li>
          </ul>
        </div>
      </div>
    </div>

  </div>

  <small class="ui horizontal inverted divider header">
    lancetw&lt;at&gt;gmail.com, 2016~2017
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
      const items = pickBy(rdata, (o) => {
        return moment(o.time).isBetween(moment().subtract(1, 'day').hour(17).minute(55), moment().add(1, 'day').hour(5).minute(55), 'minute', '[)')
      })
      if (!isEmpty(items)) this.items5 = items

      this.loading2 = false
    }, (errors) => {
      console.log(errors)
    })

    this.loading3 = true
    this.$http.get(serverAddress + '/api/news/v1/typhon').then((response) => {
      const rdata = sortBy(response.data.news, (o) => { return o.time })
      const items = pickBy(rdata, (o) => {
        return moment(o.time).isBetween(moment().subtract(1, 'day').hour(17).minute(55), moment().add(1, 'day').hour(5).minute(55), 'minute', '[)')
      })
      if (!isEmpty(items)) this.items6 = items

      this.loading3 = false
    }, (errors) => {
      console.log(errors)
    })

    this.loading4 = true
    this.$http.get(serverAddress + '/api/news/v1/earthquake').then((response) => {
      const rdata = sortBy(response.data.news, (o) => { return o.time })
      const items = pickBy(rdata, (o) => {
        return moment(o.time).isBetween(moment().subtract(1, 'day').hour(17).minute(55), moment().add(1, 'day').hour(5).minute(55), 'minute', '[)')
      })
      if (!isEmpty(items)) this.items7 = items

      this.loading4 = false
    }, (errors) => {
      console.log(errors)
    })

    this.loading5 = true
    this.$http.get(serverAddress + '/api/news/v1/hcfd').then((response) => {
      const rdata = sortBy(response.data.news, (o) => { return o.time })
      const items = pickBy(rdata, (o) => {
        return moment(o.time).isBetween(moment().subtract(1, 'day').hour(5).minute(55), moment().add(1, 'day').hour(5).minute(55), 'minute', '[)')
      })
      if (!isEmpty(items)) this.items8 = items

      this.loading5 = false
    }, (errors) => {
      console.log(errors)
    })

    const keywords0 = '火警|火災|火光|火球|大火|失火|救火|起火|打火|燒車|瓦斯味|濃煙|大煙|黑煙|消防局|消防隊|消防人員|消防車|燃燒|救災|滅火|火場|火勢|救護車|翻覆|受困'
    const keywords1 = '竹市.*火警|火警.*竹市|竹市.*火災|火災.*竹市|竹市.*火光|火光.*竹市|竹市.*火球|火球.*竹市|竹市.*大火|大火.*竹市|竹市.*失火|失火.*竹市|竹市.*救火|救火.竹市|竹市.*起火|起火.*竹市|竹市.*打火|打火.*竹市|竹市.*燒車|燒車.*竹市|竹市.*瓦斯味|瓦斯味.*竹市|竹市.*濃煙|濃煙.*竹市|竹市.*大煙|大煙.*竹市|竹市.*黑煙|黑煙.*竹市|竹市.*消防局|消防局.*竹市|竹市.*消防隊|消防隊.*竹市|竹市.*消防人員|消防人員.*竹市|竹市.*消防車|消防車.*竹市|竹市.*燃燒|燃燒.*竹市|竹市.*救災|救災.*竹市|竹市.*火場|火場.*竹市|竹市.*救護車|救護車.*竹市|竹市.*火勢|火勢.*竹市|風城.*消防|消防.*風城|竹市.*翻覆|翻覆.*竹市|竹市.*受困|受困.*竹市'
    const keywords2 = '新竹.*火警|火警.*新竹|新竹.*火災|火災.*新竹|新竹.*火光|新竹.*新竹|新竹.*火球|火球.*新竹|新竹.*大火|大火.*新竹|新竹.*失火|失火.*新竹|新竹.*救火|救火.新竹|新竹.*起火|起火.*新竹|新竹.*打火|打火.*新竹|新竹.*燒車|燒車.*新竹|新竹.*瓦斯味|瓦斯味.*新竹|新竹.*濃煙|濃煙.*新竹|新竹.*大煙|大煙.*新竹|新竹.*黑煙|黑煙.*新竹|新竹.*消防局|消防局.*新竹|新竹.*消防隊|消防隊.*新竹|新竹.*消防人員|消防人員.*新竹|新竹.*消防車|消防車.*新竹|新竹.*燃燒|燃燒.*新竹|新竹.*救災|救災.*新竹|新竹.*火場|火場.*新竹|新竹.*救護車|救護車.*新竹|新竹.*火勢|火勢.*新竹|風城.*消防|消防.*風城|新竹.*翻覆|翻覆.*新竹|新竹.*受困|受困.*新竹'

    // 新竹大小事
    this.$http.get(serverAddress + '/api/facebook/v1/feed/1507207486163325?include=' + keywords0).then((response) => {
      const rdata = sortBy(response.data.fb, (o) => { return o.time })
      const items = pickBy(rdata, (o) => {
        return moment(o.time).isBetween(moment().subtract(1, 'day').hour(17).minute(55), moment().add(1, 'day').hour(5).minute(55), 'minute', '[)')
      })
      if (!isEmpty(items)) this.items9 = Object.assign({}, this.items9, items)
    }, (errors) => {
      console.log(errors)
    })

    // 新竹人新竹事
    this.$http.get(serverAddress + '/api/facebook/v1/feed/123595078051928?include=' + keywords0).then((response) => {
      const rdata = sortBy(response.data.fb, (o) => { return o.time })
      const items = pickBy(rdata, (o) => {
        return moment(o.time).isBetween(moment().subtract(1, 'day').hour(17).minute(55), moment().add(1, 'day').hour(5).minute(55), 'minute', '[)')
      })
      if (!isEmpty(items)) this.items9 = Object.assign({}, this.items9, items)
    }, (errors) => {
      console.log(errors)
    })

    // 新竹爆料公社
    this.$http.get(serverAddress + '/api/facebook/v1/feed/1695176847369554?include=' + keywords0).then((response) => {
      const rdata = sortBy(response.data.fb, (o) => { return o.time })
      const items = pickBy(rdata, (o) => {
        return moment(o.time).isBetween(moment().subtract(1, 'day').hour(17).minute(55), moment().add(1, 'day').hour(5).minute(55), 'minute', '[)')
      })
      if (!isEmpty(items)) this.items9 = Object.assign({}, this.items9, items)
    }, (errors) => {
      console.log(errors)
    })

    // 靠北消防
    this.$http.get(serverAddress + '/api/facebook/v1/feed/374097612788175?include=' + keywords1).then((response) => {
      const rdata = sortBy(response.data.fb, (o) => { return o.time })
      const items = pickBy(rdata, (o) => {
        return moment(o.time).isBetween(moment().subtract(1, 'day').hour(17).minute(55), moment().add(1, 'day').hour(5).minute(55), 'minute', '[)')
      })
      if (!isEmpty(items)) this.items9 = Object.assign({}, this.items9, items)
    }, (errors) => {
      console.log(errors)
    })

    // 爆料公社粉絲頁
    this.$http.get(serverAddress + '/api/facebook/v1/feed/162608724089621?type=pg&include=' + keywords1 + '|' + keywords2).then((response) => {
      const rdata = sortBy(response.data.fb, (o) => { return o.time })
      const items = pickBy(rdata, (o) => {
        return moment(o.time).isBetween(moment().subtract(1, 'day').hour(17).minute(55), moment().add(1, 'day').hour(5).minute(55), 'minute', '[)')
      })
      if (!isEmpty(items)) this.items9 = Object.assign({}, this.items9, items)
    }, (errors) => {
      console.log(errors)
    })

    // 看見新竹粉絲頁
    this.$http.get(serverAddress + '/api/facebook/v1/feed/Seehsinzhu?type=pg&include=' + keywords1 + '|' + keywords2).then((response) => {
      const rdata = sortBy(response.data.fb, (o) => { return o.time })
      const items = pickBy(rdata, (o) => {
        return moment(o.time).isBetween(moment().subtract(1, 'day').hour(17).minute(55), moment().add(1, 'day').hour(5).minute(55), 'minute', '[)')
      })
      if (!isEmpty(items)) this.items9 = Object.assign({}, this.items9, items)
    }, (errors) => {
      console.log(errors)
    })

    // 非公開社團 atom
    this.$http.get(serverAddress + '/api/blogger/v1/feed/default?include=' + keywords1 + '|' + keywords2).then((response) => {
      const rdata = sortBy(response.data.feed, (o) => { return o.time })
      const items = pickBy(rdata, (o) => {
        return moment(o.time).isBetween(moment().subtract(1, 'day').hour(17).minute(55), moment().add(1, 'day').hour(5).minute(55), 'minute', '[)')
      })
      if (!isEmpty(items)) this.items10 = Object.assign({}, this.items10, items)
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
      items8: [],
      items9: [],
      items10: []
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
  font-size: 1.35rem;
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
  color: #666;
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
  color: #666;
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

#fb {
  font-family: "標楷體", DFKai-SB, BiauKai, STKaiti;
  font-size: 1.35rem;
  text-align: center;
  color: #000;
}

#fb p {
  text-align: left;
}

#fb ul {
  margin: 0;
  padding: 0;
  line-height: auto;
  text-align: left;
}

#fb ul li {
  margin: 0;
  padding: 0;
  line-height: auto;
  font-weight: normal;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

#fb ul li a {
  margin: 0;
  padding: 0;
  text-decoration: none;
  color: #333 !important;
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
