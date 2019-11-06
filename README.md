## BEM
这些辅助工具的设计使开发人员能够使用 SCSS 构造良好和一致的 BEM 组件。 Bem 代表“块元素 -- 修饰符” ，描述了一种类名语法结构，旨在保持代码模块化。

## Scss Mixins

```scss
@charset "UTF-8";

$bem_separator_element: '__';
$bem_separator_modifier: '--';
$namespace: 'qqf';

/* BEM */
@mixin b($bem_item) {
  $B: $bem_item!global;
  .#{$namespace + '-' + $bem_item} {
    @content
  }
}

@mixin e($bem_element) {
  $bem_parent: &;
  // 检查父选择器是否是一个修饰符, 如果是将生成一个 块名--修饰符, 并且在内部包括 块名__元素名
  // 如果不是的话, 将直接创建一个块名 块名__元素名
  $bem_is_parent: str_index(#{$bem_element}, #{$bem_separator_modifier});
  @if $bem_is_parent != null {
    $bem_parent_without_modifier: str_slice(#{$bem_parent}, 0, $bem_is_parent - 1);
    #{$bem_parent_without_modifier}#{$bem_separator_element}#{$bem_element} {
      @content
    }
  } @else {
    @at-root {
      #{&}#{$bem_separator_element}#{$bem_element} {
        @content
      }
    }
  }
}

@mixin m($bem_modifier) {
  $bem_parent: &;
  @at-root {
    #{$bem_parent}#{$bem_separator_modifier}#{$bem_modifier} {
      @content;
    }
  }
}
```

## Reference
[bem.scss](https://github.com/winstromming/bem.scss)