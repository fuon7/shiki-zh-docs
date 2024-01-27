---
outline: deep
---

# 迁移

Shiki 的 v1.0 版本是一次重大重写，我们借此机会修改了过去的所有设计决定。我们原本有一个独立的软件包名称 [Shikiji](https://github.com/antfu/shikiji)，用来试验新的设计，现在合并回 Shiki，成为 v1.0。

## 从 v0.14 迁移

与 [`shiki@0.14.3`](https://github.com/shikijs/shiki/releases/tag/v0.14.3) 相比，破坏性更改列表内容如下：

### 硬性破坏性改动

你必须手动迁移的破坏性改动：

- CJS 和 IIFE 构建被移除。查看 [使用 CJS](/guide/install#cjs-usage) 和 [使用 CDN](/guide/install#cdn-usage) 获取更多详细信息。
- `codeToHtml` 在内部使用了 [`hast`](https://github.com/syntax-tree/hast)。 生成的 HTML 会略有不同，但行为一致。
- 不支持 `css-variables` 主题。请使用 [双主题](/guide/dual-themes)，或在 [主题颜色控制](/guide/theme-colors) 查看更多。

### 软性破坏性改动

`shiki` 包中包含的破坏性改动，而 [兼容构建 `@shikijs/compat`](/guide/compat#compatibility-build) 中不具备（屏蔽）:

- 顶级命名导出项 `setCDN`、`loadLanguage`、`loadTheme` 和 `setWasm` 被移除，因为其不再被需要。
- `BUNDLED_LANGUAGES`、`BUNDLED_THEMES` 被移动至 `shikiji/langs` 和 `shikiji/themes` 中并分别更名为 `bundledLanguages` 和 `bundledThemes`。
- `getHighlighter` 的 `theme` 选项被移除，请改用数组形式的 `themes`。
- 高亮显示器不再具有内部的默认主题上下文。 对于 `codeToHtml` 和 `codeToThemedTokens`，`theme` 选项是必须的。
- `codeToThemedTokens` 默认情况下将 `includeExplanation` 设置为 `false`。
- `.ansiToHtml` 作为一个特殊的语言 `ansi` 被合并至 `.codeToHtml`。请使用 `.codeToHtml(code, { lang: 'ansi' })`。
- `lineOptions` 被移除，取而代之的是完全可定制的 `transforms` 选项。
- `LanguageRegistration` 的 `grammar` 字段被展开到 `LanguageRegistration` 本身，参考类型定义获取详细信息。

## 从 Shikiji 迁移

如果你已经在使用 [Shikiji](https://github.com/antfu/shikiji)，请确保你使用的是最新的次版本 v0.10。然后重新命名软件包，这个迁移的过程应该会非常简单：

- `shikiji` -> `shiki`
- `shikiji-core` -> `@shikijs/core`
- `shikiji-twoslash` -> `@shikijs/twoslash`
- `shikiji-transformers` -> `@shikijs/transformers`
- `shikiji-monaco` -> `@shikijs/monaco`
- `shikiji-cli` -> `@shikijs/cli`
- `markdown-it-shikiji` -> `@shikijs/markdown-it`
- `rehype-shikiji` -> `@shikijs/rehype`