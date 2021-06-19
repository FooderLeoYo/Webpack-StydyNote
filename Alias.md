# Alias

## 目录

[为什么要使用别名](#jump1)

[webpack.config.js](#jump2)

[tsconfig.json](#jump3)

[css的@import](#jump4)

[](#jump)

[](#jump)

---	

<span id="jump1"></span>

## 为什么要使用别名

由于项目中代码层级比较深，所以如果采用相对路径，相互之间引用起来会比较麻烦

例如：

```javascript
import utils from '../../../../../utils'
```

别名的作用就是省略这些```../```或```./```，使得路径更简洁明了。例如：

```javascript
import utils from '@utils'
```

下面就需要配置的文件逐步进行说明

---

<span id="jump2"></span>

## webpack.config.js

在```resolve```内添加```alias```

格式为：```'别名'： path.resolve(__dirname, '路径')```

根路径即```webpack.config.js```自身所在位置

例如：

```javascript
const baseWebpackConfig = {
  resolve: {
    alias: {
      '@api': path.resolve(__dirname, '../src/api/'),
      '@assets': path.resolve(__dirname, '../src/assets/'),
      '@components': path.resolve(__dirname, '../src/components/')
    },
  // 其他配置……
  },
  // 其他配置……
}
```

---

<span id="jump3"></span>

## tsconfig.json

如果项目使用的是TypeScript，则还需要配置此文件

在```"compilerOptions"```内添加```"baseUrl"```和```"paths"```：

### "baseUrl"

按```tsconfig.json```自身所在位置为```./```，可使用相对路径的方式，将```baseUrl```设置为任意位置，如：

```javascript
"baseUrl": "../assets/img",
```

```"baseUrl"```是```"paths"```的根路径，```"paths"```将相对于它进行解析

因此必须设置```"baseUrl"```，哪怕是以```tsconfig.json```自身所在位置作为```"baseUrl"```，也要写成：

```javascript
"baseUrl": "./",
// 或
"baseUrl": ".",
```

### "paths"

用来设置别名及其对应的路径，格式为：```"别名/*": ["路径/*"]```

例如：

```javascript
"@src/*": [ "src/*" ],
```

### 范例

```javascript
// tsconfig.json
{
  "compilerOptions": {
    "baseUrl": "./",
    "paths": {
      "@src/*": [
        "src/*"
      ],
      "@api/*": [
        "src/api/*"
      ],
      "@components/*": [
        "src/components/*"
      ]
    },
    // 其他配置……
  },
  // 其他配置……
}
```

---

<span id="jump4"></span>

## css的@import

需要在别名前加```~```

例如：

```css
@import "~@assets/stylus/px2rem.styl"
```
