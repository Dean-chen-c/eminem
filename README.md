> 马绍尔·布鲁斯·马瑟斯三世（英语：Marshall Bruce Mathers III，1972 年 10 月 17 日－），知名于其艺名埃米纳姆（Eminem），是一位美国著名说唱歌手、词曲作家、唱片制作人、演员及电影制作人。他一直被认为是嘻哈史上最伟大，最有影响力的说唱歌手，也被称为“说唱之神”(Rap God)。

eminem 是一个 webpack 启动器，它将繁杂的 webpack 配置分解并且收敛在一个 package 中。

- [快速开始 ✨](#快速开始-)
- [使用方式: 🎨](#使用方式-)
- [自定义配置 🎠](#自定义配置-)
- [插件 🎁](#插件-)
- [其他选项 🧨](#其他选项-)

目前已经可以正常使用，但功能正在优化中，新特性也会陆续增加。

#### 快速开始 ✨

```bash
npm i @eminemjs/cli -g
em init my-app
```

通过 `--help`查看命令帮助

#### 使用方式: 🎨

```bash
 // 在当前文件夹下生成项目
 em init .
 // 使用yarn
 em init my-app --useYarn
 // 使用淘宝源
 em init my-app --usecnpm
 // 使用模板
 em init my-app --template=@eminemjs/react-template 
```

#### 自定义配置 🎠

```javascript
const web = require('@eminemjs/addons/presets/web'); // 内置提供了 vanilla web  和 react web 的配置
module.exports = {
    apps: [
        {
            entry: 'app/index.js',
            template: 'index.html',
            name: 'index'
        }
    ],
    use: [web(),(context)=>{

        // do something

        //! 一定要返回context
        return context

    }]
};

```
#### 插件 🎁
插件其实就是webpack的配置集合，比如内置的 web 和 react 预设就是一种插件,在使用时要注意顺序，后置的插件可能会修改前面的插件返回的context
```javascript
const react = require('@eminemjs/addons/presets/react'); 
const webp = require('@eminemjs/addons/middleware/webp'); 
module.exports = {
    apps: [
        {
            entry: 'app/index.js',
            template: 'index.html',
            name: 'index'
        }
    ],
    use: [react(),webp()]
};

```

#### 其他选项 🧨
 - app 程序的入口文件(从src目录开始)和html模板文件(从public目录开始)
 - sourceMap 是否生成sourcce map文件
 - strict 默认情况下,构建过程中如果代码中存在lint警告或错误将导致build失败，这是为了强制使用统一的代码规范，如果你对此感到绝望，可是将此选项设为false以关闭该检查
