# 快速开始 quick-start

## 快速开始

### 克隆代码
我们只要拉取 `monoweb-docs` 分支代码。

```bash
git clone -b monoweb-docs git@bitbucket.org:ciandt_it/enterprise-cms.git
```


### 安装依赖
1. Install yarn using `npm install yarn -g`
2. Install lerna using `npm install lerna -g`
3. 进入目录 `enterprise-cms/monoweb/frontend/` 执行安装 `yarn install`

```bash
yarn install
```

4. Run `lerna bootstrap` to install, link and setup the monorepo.
5. You now have to compile the packages by running `yarn run lib:compile`

### 运行项目
**Run development server:**
```bash
yarn workspace @fctg/applications-nextjs-rich-pages dev
```
**访问组件 button 页面**
http://localhost:3000/p/components/button

### Navigate pages
While runing the server, open the local environment in the browser to see the result, example:
- http://localhost:3000/p/en-au/fc/rich_pages/our-promise
- http://localhost:3000/p/en-au/fc/blogs
- http://localhost:3000/p/en-au/fc/blogs/australia/first-blog-test

Similarly, mock pages can be loaded for further testing:
- http://localhost:3000/p/catalogue

A list of available componentes can be found under `/src/componentMaps/components/`, example:

- http://localhost:3000/p/components/accordion
- http://localhost:3000/p/components/button
- http://localhost:3000/p/components/video


test develop