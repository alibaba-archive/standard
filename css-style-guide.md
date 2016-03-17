## CSS Style Guide

毫不夸张地说，这份指南会使你变得更优秀，从更优雅的代码上体现

自从新的 [TB-UI](https://github.com/teambition/TB-UI) 站在 [Stylus](http://stylus-lang.com), [SMACSS](https://smacss.com/), [OOCSS](http://oocss.org/), [Bootstrap](getbootstrap.com) 的肩膀上后

必须有一份风格指南才能驾驭好它们，从而[站上去看得更远](https://en.wikipedia.org/wiki/Standing_on_the_shoulders_of_giants)

> "Consistent code, even when written by a team, should look like one person wrote it."
>
>  ~ [Addy Osmani](https://addyosmani.com/blog/javascript-style-guides-and-beautifiers/)

除了 Addy Osmani 所说的人团合一，本指南更侧重培养良好的习惯

绝不会像 [CSS Guidelines](http://cssguidelin.es/) 这样细而全的手册让你怀疑自我的记忆力

毕竟人生苦短，简洁至上，就算是指南也得讲求[基本法](https://medium.com/@jontomato/keep-your-style-guide-simple-1a1bf00cfc60#.q74234ylf)

## TL;DR

如果你是一个极度崇尚自由的人，你大可不必去阅读或修订这些指南

追随自己的内心，把指南中会束缚你的条目交给 [TB-Linter](https://github.com/teambition/TB-Linter) 去遵守

## Table of Contents

- [Terminology](#terminology)
- [Indentation & Spacing](#indentation--spacing)
- [Comments](#comments)
- [Declarations Ordering](#declarations-ordering)
- [Files Organization](#files-organization)
- [Media Queries](#media-queries)
- [Mixin & Variable](#mixin--variable)
- [Selector Naming & Nesting](#selector-naming--nesting)
- [Units & Dimensions](#units--dimensions)
- [Miscellaneous](#miscellaneous)

## Terminology

```CSS
/* Rule Set (the entire chunk of code below can just be referred to as a single 'rule') */

/* Selectors */
#my-id, .my-class {
  /* Declaration */
  /* Property */border: /* Value */1px solid #DCDDDE;
}
```

```Stylus
// Rule Set in Stylus

.selector
  // Declaration = Property + Value
  property: value
```

更多术语参考：[CSS Terms and Definitions](http://www.impressivewebs.com/css-terms-definitions/)

## Indentation & Spacing

- Use 2 spaces for indentation. Don't use tab.
- Remove all spaces at the end of the line.
- Use space between property and value.
- Always leave a blank line between rule sets.

Stylus 无 Braces 语法下，不再是 [Free-form language](https://en.wikipedia.org/wiki/Free-form_language)，缩进不对会直接抛出语法错误

## Comments

- 提倡[文档](http://docs.teambition.com/ui)，反对[大段的注释](http://blog.codinghorror.com/coding-without-comments/)
- 尽量保持代码的可读性，实在不行则用 TODO 或 FIXME 来标明
- 单行注释 `//` 比 `/**/` 更受欢迎

## Declarations Ordering

多条声明应该被[分组](https://smacss.com/book/formatting)和[排序](http://webdesign.tutsplus.com/articles/outside-in-ordering-css-properties-by-importance--cms-21685?utm_source=tuicool&utm_medium=referral)，根据声明作用来分：

- Display: display, visibility, opacity, float...
- Position: position, top, left...
- Box Model: width, pading, border, margin...
- Background: background-color, background-image...
- Text: line-height, font-* properties...
- Other: filter, animation, transition...

激动人心的消息，[TB-Linter](https://github.com/teambition/TB-Linter) 将会引入 [CSScomb](https://github.com/csscomb/csscomb.js) 来代替手动排序

## Files Organization

根据 [SMACSS](http://smacss.com/) 与 [Teambition](https://teambition.com) 产品的实际情况，样式文件被以下几层：

- Variables 层：全局变量
- Mixins & Functions & Utilities 层：各种全局工具与函数
- Bases 层：重置样式，基础样式
- Effects 层：特效 // 尽可能的少
- Generics 层：不含 JavaScript 交互的基础组建
- UIs 层：包含 JavaScript 交互的基础组建
- Themes 层：主题样式
- Components：包含逻辑的组建，可继承自基础组建

Tip: 不被 DOM 调用或者不生成规则的文件用下划线作为前缀

## Media Queries

根据[已经过时的](https://medium.com/intercom-inside/why-mobile-first-is-outdated-f10a3dc357bd#.l0zg89z3i) [Mobile First](http://bradfrost.com/blog/web/mobile-first-responsive-web-design/) 原则，Media Queries 的顺序为：

```Stylus
@media (min-width: $screenXS)
  @media (max-width: 500px)
@media (min-width: $screenSM)
@media (max-width: $screenLGMax)
@media (max-width: $screenMDMax)
```

Min 从小到大，Max 从大到小，Min 里面可以嵌套 Max

## Mixin & Variable

[Autoprefixer](https://github.com/postcss/autoprefixer) 的诞生，解决了厂商前缀兼容的问题，成功解放了海马

如果框架中充满大量（50 个）全局的 Mixin 与 Variable，是应该被反对的

在写业务逻辑时，不能过早考虑 [DRY](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself) 原则，优先考虑局部的复用

- Mixin 与 Variable 采用驼峰命名法
- Variable 名字使用 $ 作为前缀

## Selector Naming & Nesting

很好奇，一个性格多么好的人才能接受 [BEM](https://en.bem.info/method/) 方法论中的命名方式

> There are only two hard things in Computer Science: cache invalidation and naming things.
>
> ~ [Phil Karlton](http://martinfowler.com/bliki/TwoHardThings.html)

为了让命名与嵌套更加简单，这里只有两个关于 3 的建议：

- 用 Hyphen 分割单词，且不要超过 3 个 // 对喜欢驼峰的人说抱歉
- 选择器中的 Combinator 不要超过 3 个

## Units & Dimensions

- 值为 0 的时，不要带单位，除了 0s
- 值介于 0～1 之间时，去掉小数点前的 0，如：.8rem
- 尺寸的单位只能为：px, rem, %
- 十六进制表示颜色时，用 6 个字符，如：#223333，而不是 #233

## Miscellaneous

- 在样式兼容上，应该多参考 [Can I use](http://caniuse.com/)，特别是 IE
- 欢迎 PR 与关于指南的讨论

## References

- [VisualDNA CSS Style Guide](https://github.com/VisualDNA/css-style-guide) - A reasonable way of creating CSS Stylesheets.
- [Evernote CSS Style Guide](https://github.com/evernote/css-style-guide) - No description...
- [Globant-UI CSS Style Guide](https://github.com/globant-ui/css-style-guide) - A mostly reasonable approach to CSS.
- [Idiomatic CSS](https://github.com/necolas/idiomatic-css#general-principles) - Principles of writing consistent, idiomatic CSS.
- [JasonSee CSS Style Guide](https://github.com/jasonsee/css-styleguide) - Handy CSS Style Guide for developers.
- [CSS Bliss](https://github.com/gilbox/css-bliss) - A CSS style guide that puts the Clean, Smart, and Simple back into CSS.
- [Integralist's Style Guides](https://github.com/Integralist/Style-Guides) - These are my own personal style guides.
- [MercadoLibre CSS Style Guide](https://github.com/mercadolibre/css-style-guide#selectors) - Set standards for writing our CSS files and components.
- [Dropbox (S)CSS Style Guide](https://github.com/dropbox/css-style-guide) - Dropbox’s (S)CSS authoring style guide.
