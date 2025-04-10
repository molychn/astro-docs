---
layout: ~/layouts/MainLayout.astro
title: 配置参考
githubURL: https://github.com/withastro/astro/blob/main/packages/astro/src/%40types/astro.ts
setup: |
  import Since from '../../../components/Since.astro';
---

下面的参考资料涵盖了 Astro 所有支持的配置选项。要了解更多关于配置 Astro 的信息，请阅读我们的[配置 Astro 指南](/zh-cn/guides/configuring-astro/)。

```js
// astro.config.mjs
import { defineConfig } from 'astro/config'

export default defineConfig({
  // 你的配置在这里...
})
```

## 顶层选项

### root

<p>

**类型**：`string`<br>
**CLI:** `--root`<br>
**默认**：`"."` (current working directory)
</p>

只有当你在项目根目录以外的目录下运行 `astro` CLI 命令时，你才应该提供该选项。通常，这个选项是通过 CLI 而不是 [Astro 配置文件](/zh-cn/guides/configuring-astro/#受支持的配置文件类型)提供的，因为 Astro 需要知道项目根目录才能找到配置文件。

如果提供相对路径（例如：`--root: './my-project'`），Astro 会根据你当前的工作目录进行解析。

#### 示例

```js
{
  root: './my-project-directory'
}
```

```bash
$ astro build --root ./my-project-directory
```

### srcDir

<p>

**类型**：`string`<br>
**默认**：`"./src"`
</p>

设置 Astro 将读取网站的目录。

这个值可以是绝对路径，也可以是相对路径。

```js
{
  srcDir: './www'
}
```

### publicDir

<p>

**类型**：`string`<br>
**默认**：`"./public"`
</p>

设置静态资源目录。这个目录下的文件在开发过程中被提供给 `/`，在构建过程中被复制到构建目录。这些文件总是按原样提供或复制的，没有转换或捆绑。

这个值可以是绝对路径，也可以是相对路径。

```js
{
  publicDir: './my-custom-publicDir-directory'
}
```

### outDir

<p>

**类型**：`string`<br>
**默认**：`"./dist"`
</p>

设置 `astro build` 将你的最终构建写入的目录。

这个值可以是绝对路径，也可以是相对路径。

```js
{
  outDir: './my-custom-build-directory'
}
```

### site

<p>

**类型**：`string`
</p>

你最终部署的链接。Astro 会使用这个完整的链接来生成网站地图和最终构建的规范链接。强烈建议你设置这个配置项，以获得 Astro 最佳体验。

```js
{
  site: 'https://www.my-site.dev'
}
```

### base

<p>

**类型**：`string`
</p>

你要部署到的基本路径。Astro 在开发过程中会匹配这个路径名，这样你的开发环境就会尽可能地与你的构建环境匹配。在下面的例子中，`astro dev` 会在 `/docs` 处启动你的服务器。

```js
{
  base: '/docs'
}
```

请注意，使用 `base` 选项后你须要更改所有的链接。在这个例子中，你须要在链接前面添加 `/docs/` 前缀。

比如，当你想要使用某张图片时，你须要将 `'/someimg.png'` 改为 `'/docs/someimg.png'`。

```astro {2}
<!-- <img src="/someimg.png">是错误的！ -->
<img src="/docs/someimg.png">
```

### trailingSlash

<p>

**类型**：`'always' | 'never' | 'ignore'`<br>
**默认**：`'ignore'`
</p>

设置设计服务器的路由匹配行为。从以下选项中选择：

- `'always'` - 只匹配包含尾部斜线的链接（例如：`/foo/`）。
- `'never'` - 不匹配包含尾部斜线的链接（例如：`/foo`）。
- `'ignore'`- 匹配链接，不管是否存在尾部的 `/`。

如果你的生产主机对尾部斜杠的工作或不工作有严格的处理方式，请使用该配置选项。

如果你希望自己更严格一些，那么你也可以设置这个选项，这样在开发过程中，无论是否有尾部斜杠的URL都不会工作。

```js
{
  // 示例：在开发过程中要求有尾部斜线
  trailingSlash: 'always'
}
```

**另见**：

- build.format

### adapter

<p>

**类型**：`AstroIntegration`
</p>

使用构建适配器将其部署到你最喜爱的服务器、无服务器或边缘主机。导入我们的第一方适配器 [Netlify](/zh-cn/guides/deploy/netlify/#adapter-for-ssredge)、[Vercel](/zh-cn/guides/deploy/vercel/#ssr-适配器)，以及更多的适配器来使用Astro SSR。

[有关 SSR 的更多信息，请参见我们的服务器端渲染指南](/zh-cn/guides/server-side-rendering/)，以及[我们的部署指南](/zh-cn/guides/deploy/)以获得完整的主机列表。

```js
import netlify from '@astrojs/netlify/functions';
{
  // 示例：使用 Netlify 无服务器部署构建
  adapter: netlify(),
}
```

**另见**：

- output

### output

<p>

**类型**：`'static' | 'server'`<br>
**默认值**：`'static'`
</p>

指定构建的输出目标。

- `static`- 构建静态网站，部署到任何静态主机上。
- `server` - 构建应用，部署到支持S SR（服务器端渲染）的主机上。

```js
import { defineConfig } from 'astro/config';

export default defineConfig({
  output: 'static'
})
```

**另见**：

- adapter

## 构建选项

### build.format

<p>

**类型**：`('file' | 'directory')`<br>
**默认**：`'directory'`
</p>

控制每个页面的输出文件格式：

- 如果是'file'，Astro将为每个页面生成一个HTML文件（例如："/foo.html"）。
- 如果是'directory'，Astro将为每个页面生成一个有嵌套的`index.html`文件的目录（例如："/foo/index.html"）。

```js
{
  build: {
    // 示例：在构建过程中生 成`page.html` 而不是 `page/index.html`。
    format: 'file'
  }
}
```

#### 对 Astro.url 的影响

设置 `build.format` 可以控制 `Astro.url` 在构建过程中被设置成什么。当它是：

- `directory` - `Astro.url.pathname` 将包括一个尾部斜杠，以模仿文件夹行为；例如 `/foo/`。
- `file` - `Astro.url.pathname` 将包括 `.html`，即`/foo.html`。

这意味着当你使用 `new URL('./relative', Astro.url)` 创建相对的连接时，开发和构建会得到一致的行为。

## 服务器选项

定制 Astro 开发服务器，适用于 `astro dev` 和 `astro preview`。

```js
{
  server: { port: 1234, host: true}
}
```

要根据运行的命令（`dev`、`preview`）设置不同的配置，也可以向这个配置选项传递函数。

```js
{
  // 示例：使用函数语法，根据命令进行定制
  server: (command) => ({ port: command === 'dev' ? 3000 : 4000 })
}
```

### server.host

<p>

**类型**：`string | boolean`<br>
**默认**：`false`<br>
<Since v="0.24.0" />
</p>

设置服务器应该监听哪些网络 IP 地址（即非本地主机 IP）。

- `false`- 不在网络 IP 地址上公开
- `true`- 侦听所有地址，包括 LAN 和公开地址
- `[custom-address]` - 在 `[custom-address]` 网络 IP 地址上公开（例如：`192.168.0.1`）。

### server.port

<p>

**类型**：`number`<br>
**默认**：`3000`
</p>

设置服务器监听端口。

如果给定的端口已经在使用，Astro 会自动尝试下一个可用的端口。

```js
{
  server: { port: 8080 }
}
```

## Markdown 选项

### markdown.drafts

<p>

**类型**：`boolean`<br>
**默认**：`false`
</p>

控制 markdown 草稿页是否应该被包含在构建中。

如果 markdown 页面在 frontmatter 中包含 `draft: true`，那么它就被认为是草稿。在开发过程中会显示草稿页（`astro dev`），但在默认情况下，它们不会被包含在你的最终构建中。

```js
{
  markdown: {
    // 示例：在你的最终构建中包括所有的草稿
    drafts: true,
  }
}
```

### markdown.shikiConfig

<p>

**类型**：`Partial<ShikiConfig>`
</p>

Shiki 配置选项。使用方法见 [markdown 配置文档](/zh-cn/guides/markdown-content/#shiki-配置)。

### markdown.syntaxHighlight

<p>

**类型**：`'shiki' | 'prism' | false`<br>
**默认**：`shiki`
</p>

可供使用的语法高亮器：

- `shiki` - 使用 [Shiki](https://github.com/shikijs/shiki) 高亮器
- `prism` - 使用 [Prism](https://prismjs.com/) 高亮器
- `false` - 不使用语法高亮。

```js
{
  markdown: {
    // 示例：在 Markdown 中使用 prism 进行语法高亮显示
    syntaxHighlight: 'prism',
  }
}
```

### markdown.remarkPlugins

<p>

**类型**：`RemarkPlugins`
</p>

通过自定义 [Remark 插件](https://github.com/remarkjs/remark)来定制 Markdown 构建方式。你可以导入并应用插件函数（推荐），或传递一个值为插件名的字符串。

:::caution
如果提供了插件列表则将**删除**所有默认插件。要保留这些默认值，请见 `extendDefaultPlugins` 标志。
:::

```js
import remarkToc from 'remark-toc';
{
  markdown: {
    remarkPlugins: [remarkToc]
  }
}
```

### markdown.rehypePlugins

<p>

**类型**：`RehypePlugins`
</p>

通过自定义 [Rehype 插件](https://github.com/remarkjs/remark-rehype) 插件来定制对你的 Markdown 输出内容的处理方式。你可以导入并应用插件函数（推荐），或传递一个值为插件名的字符串。

:::caution
如果提供了插件列表则将**删除**所有默认插件。要保留这些默认值，请见 `extendDefaultPlugins` 标志。
:::

```js
import rehypeMinifyHtml from 'rehype-minify';
{
  markdown: {
    rehypePlugins: [rehypeMinifyHtml]
  }
}
```

### markdown.extendDefaultPlugins

<p>

类型：`boolean`<br>
默认值：`false`
</p>

Astro 默认应用 [GitHub-flavored Markdown](https://github.com/remarkjs/remark-gfm) 和 [Smartypants](https://github.com/silvenon/remark-smartypants) 插件。当添加你自己的 remark 或 rehype 插件时，你可以通过将 `extendDefaultPlugins` 标志为 `true` 来保留这些默认值。

```js
{
  markdown: {
    extendDefaultPlugins: true,
    remarkPlugins: [exampleRemarkPlugin],
    rehypePlugins: [exampleRehypePlugin],
  }
}
```

### markdown.remarkRehype

<p>

**类型**：`RemarkRehype`
</p>

向 [remark-rehype](https://github.com/remarkjs/remark-rehype#api) 传递选项。

```js
{
  markdown: {
    // 示例：将脚注文本翻译成另一种语言，这里是默认的英文内容
    remarkRehype: { footnoteLabel: "Footnotes", footnoteBackLabel: "Back to content"},
  },
};
```

## 集成

用自定义集成来扩展 Astro 功能。你可以用集成来添加框架支持（如 Solid.js）、新功能（如站点地图）和新库支持（如 Partytown 和 Turbolinks）。

请阅读我们的[集成指南](/zh-cn/guides/integrations-guide/)，以帮助开始使用Astro集成。

```js
import react from '@astrojs/react';
import tailwind from '@astrojs/tailwind';
{
  // 示例：添加 React + Tailwind 支持
  integrations: [react(), tailwind()]
}
```

## Vite

传递额外的配置选项给 Vite。适用于需要使用一些 Astro 不支持的高级配置。

在 [vitejs.dev](https://vitejs.dev/config/) 上查看完整的 `vite` 配置对象文档。

#### 示例

```js
{
  vite: {
    ssr: {
      // 示例；如果需要的话，可以强制破坏性包跳过 SSR 处理
      external: ['broken-npm-package'],
    }
  }
}
```

```js
{
  vite: {
    // 示例：直接在 Astro 项目中添加自定义 Vite 插件
    plugins: [myPlugin()],
  }
}
```

## Legacy 标志

为了帮助一些用户在 Astro 不同版本之间进行迁移，我们偶尔会引入 `legacy` 标志。
这些标志允许你在最新的版本中选择使用 Astro 的一些废弃的或其他过时的行为，
这样你就可以继续升级并使用新的 Astro 版本。

### legacy.astroFlavoredMarkdown

<p>

**类型**：`boolean`<br>
**默认值**：`false`<br>
<Since v="1.0.0-rc.1" />
</p>

启用 Astro pre-v1.0 对 `.md` Markdown 文件中的组件和 JSX 表达式的支持。
在 Astro `1.0.0-rc` 中，默认移除了这种原始的行为，以支持我们新的 [MDX集成](/zh-cn/guides/integrations-guide/mdx/)。

要启用这一行为，请在 [`astro.config.mjs` 配置文件](/zh-cn/guides/configuring-astro/#astro-配置文件)中将 `legacy.astroFlavoredMarkdown` 设置为 `true`。

```js
{
  legacy: {
    // 示例：增加对传统 Markdown 功能的支持
    astroFlavoredMarkdown: true,
  },
}
```
