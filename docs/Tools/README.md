# 优质工具总览

> 记录目前在 `monoweb` 中使用过的 开发小工具
- [JSON Editor](https://codebeautify.org/online-json-editor)

<div class="list-unstyled row row-cols-1 row-cols-sm-1 row-cols-md-2 row-cols-lg-3 g-3">
  <template v-for="(item, index) in tool">
    <div class="col" v-if="index > 0">
      <div class="card" style="height: 15rem;" >
        <div class="card-body" style="display: flex; flex-direction: column;">
          <h5 class="card-title">{{index}}: {{ item.title }}</h5>
          <p class="card-text" style="flex: 1">{{ item.message }}</p>
          <div class="card-fooer">
            <a :href="item.url" class="btn btn-primary text-light btn-sm" target="_blank">工具站点</a>
            <a v-if="item.localdoc" :href="'#/Tools/'+item.localdoc" target="_blank" class="btn btn-link btn-sm">本地文档 </a>
          </div>
        </div>
      </div>
    </div>
  </template>
</div>



