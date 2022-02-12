优化目的：减少打包时间，提升页面性能

- 压缩资源，减少文件体积，提升页面加载速度
  - js文件压缩 terser-webpack-plugin
  - css文件压缩 css-minimizer-webpack-plugin
- 控制打包作用范围，避免不需要webpack处理的模块也被处理的时间浪费
  - loader 配置 exclude或者include
  - 设置模块noParse，例如lodash不需要被loader处理，可以设置 module: { noParse: /lodash/ }
  - 设置resolve.modules，指定webpack如何搜寻依赖，如 module.exports = { resolve: { modules: [path.resolve(__dirname, 'node_modules')] } }指定webpack从当前目录的node_modules里寻找依赖，如果找不到依赖则直接报错（若不设置的话，找不到依赖则可能去上层继续找，浪费时间）
- 代码分割
  - 多入口 手动分割代码
  - import动态加载
  - splitChunks抽取公共代码 插件 splitChunksPlugin
- tree shaking 打包时检测没有使用的代码，并将未使用的代码移除，减少打包体积 1.标识未使用代码 2.移除未使用代码 。 生产环境自动开启tree shaking
- 使用缓存
  - 缓存可以使得第一次后的构建时间减少，提升开发体验，webpack5以前需要借助cache-loader,dll动态链接技术做缓存处理， webpack5提供了持久化缓存只需设置cache: { type: 'filesystem' }即可开启文件系统缓存，type可支持多种配置