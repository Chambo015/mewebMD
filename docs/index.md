<!-- ---
hide:
  - navigation
  - toc

--- -->

# Главная

For full documentation visit [mkdocs.org](https://www.mkdocs.org).

## Commands

* `mkdocs new [dir-name]` - alalalal.
* `mkdocs serve` - Start the live-reloading docs server.
* `mkdocs build` - Build the documentation site.
* `mkdocs -h` - Print help message and exit.

## Project layout

    mkdocs.yml    # The configuration file.
    docs/
        index.md  # The documentation homepage.
        ...       # Other markdown pages, images and other files.


Lorem ipsum dolor sit amet, consectetur adipiscing elit. Etiam a turpis ut nisl suscipit imperdiet. Phasellus molestie vitae mi et pulvinar. Cras gravida vitae odio vel mollis. Praesent lacinia vehicula nibh, vel bibendum sapien dapibus a. Nam tempor augue nec nulla finibus, quis fringilla tortor pellentesque. Quisque tincidunt molestie lobortis. Aliquam malesuada eros nec metus fringilla, ut vulputate dolor efficitur. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vestibulum convallis efficitur metus.

Fusce feugiat accumsan odio ac commodo. Maecenas euismod fringilla vehicula. Maecenas vel sapien quis lacus tincidunt faucibus at eget erat. Suspendisse mollis justo eget velit dictum sagittis. Pellentesque at euismod ante, sit amet euismod ex. Duis id velit commodo, tempor purus finibus, malesuada enim. Fusce scelerisque blandit nisi, eget egestas diam maximus in. Ut quis lorem et est congue dictum. Morbi mollis lorem quis lorem varius, non pretium enim facilisis. Fusce justo turpis, euismod quis molestie vel, placerat et mauris. Aenean id neque at ipsum euismod tempor vel finibus metus. Sed blandit vulputate sem, sollicitudin luctus ligula sodales at. Nulla facilisi.

Lorem Ipsum - это текст-"рыба", часто используемый в печати и вэб-дизайне. Lorem Ipsum является стандартной "рыбой" для текстов на латинице с начала XVI века. В то время некий безымянный печатник создал большую коллекцию размеров и форм шрифтов, используя Lorem Ipsum для распечатки образцов. Lorem Ipsum не только успешно пережил без заметных изменений пять веков, но и перешагнул в электронный дизайн. Его популяризации в новое время послужили публикация листов Letraset с образцами Lorem Ipsum в 60-х годах и, в более недавнее время, программы электронной вёрстки типа Aldus PageMaker, в шаблонах которых используется Lorem Ipsum.

## Примечания

!!! success "Успешно"

    Lorem Ipsum - это текст-"рыба", часто используемый в печати и вэб-дизайне. Lorem Ipsum является стандартной "рыбой" для текстов на латинице с начала XVI века. В то время некий безымянный печатник создал большую коллекцию размеров и форм шрифтов, используя Lorem Ipsum для распечатки образцов. Lorem Ipsum не только успешно пережил без заметных изменений пять веков, но и перешагнул в электронный дизайн. Его популяризации в новое время послужили публикация листов Letraset с образцами Lorem Ipsum в 60-х годах и, в более недавнее время, программы электронной вёрстки типа Aldus PageMaker, в шаблонах которых используется Lorem Ipsum.


!!! note ""

    Примечание без значка и заголовка
    Как и в случае с заголовком , значок и заголовок можно полностью исключить, добавив пустую строку непосредственно после квалификатора типа.

??? note

    Когда Детали включены и блок предупреждения начинается с ???вместо !!!, предупреждение отображается как сворачиваемый блок с небольшим переключателем с правой стороны:
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod
    nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor
    massa, nec semper lorem quam in massa.

:octicons-heart-fill-24:{ .heart }

!!! info inline end

    inline+ end справа
    inline слева
    использующие inlineмодификаторы, должны быть объявлены до блока контента, рядом с которым вы хотите их разместить.

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod
nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor
massa, nec semper lorem quam in massa.        
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod
nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor
massa, nec semper lorem quam in massa.         Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod
nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor
massa, nec semper lorem quam in massa.                              


<figure markdown>
  ![Image title](https://dummyimage.com/600x400/){ width="300" }
  <figcaption>Image caption</figcaption>
</figure>

flowchart TD
    Start --> Stop

``` mermaid
graph LR
  A[Start] --> B{Error?};
```

Option<span style="display: inline-block"></span>    | Type   | Default               | Description
:------------------------ | ------ | ----------------------| -----------
`css_class`               | string | `#!py3 'highlight`    | Default class to apply to the wrapper element on code blocks. Other extensions can override this.
`guess_lang`              | bool   | `#!py3 False`         | Guess what syntax language should be used if no language is specified. 
`pygments_style`          | string | `#!py3 'default'`     | Set the Pygments' style to use.  This really only has an effect when used with `noclasses`.
`noclasses`               | bool   | `#!py3 False`         | This will cause the styles to directly be written to the tag's style attribute instead of requiring a stylesheet.
`use_pygments`            | bool   | `#!py3 True`          | Controls whether Pygments (if available) is used to style the code, or if the code will just be escaped and prepped for a JavaScript syntax highlighter.
`linenums`                | bool   | `#!py3 None`          | Enable line numbers globally for *block* code.  This will be ignored for *inline* code. If set to `#!py3 False` line numbers will be disabled globally and can not be turned on, not even per code block.
`linenums_special`        | int    | `#!py3 1`             | Globally sets the specified nth lines' gutter with the class "special".  This can be overridden in [SuperFences](./superfences.md) per fence if desired.
`linenums_style`          | string | `#!py3 'table'`       | Controls the output style when `linenums` are enabled. Supported styles are Pygments default `table` and `inline`, but also supported is the pymdown-extensions `pymdownx-inline` which provides a special inline mode, see [Line Number Styles](#line-number-styles) for more info.
`linenums_class`          | string | `#!py3 'linenums'`    | Controls the name of the line number class when Pygments is not used.
`extend_pygments_lang`      | list   | `#!py3 []`            | A list of extended languages to add.  See [Extended Pygments Lexer Options](#extended-pygments-lexer-options) for more info.
`language_prefix`         | string | `#!py3 'language-'`   | Controls the prefix applied to the language class when Pygments is not used. By default, uses the HTML5 prefix of `language-`.
`code_attr_on_pre`        | bool   | `#!py3 False`         | By default, the language class and all attributes added via the [`attr_list`][attr-list] extension are attached to the `#!html <code>` element. This forces them to be attached to the `#!html <pre>` element.
`auto_title`              | bool   | `#!py3 False`         | When using Pygments, for all code blocks generate a title header with the name of the lexer being used. The lexer name is pulled directly from Pygments and title cased appropriately.
`auto_title_map`          | dict   | `#!py3 {}`            | A dictionary used to override certain titles returned by `auto_title`. Simply specify the title to override as the key and the desired title as the value.
`line_spans`              | string | `#!py3 ''`            | Controls the Pygments option of a similar name. If set to a nonempty string, e.g. `foo`, the formatter will wrap each output line in a `#!html <span>` tag with an id of `foo-<code_block_number>-<line_number>`.
`anchor_linenums`         | bool   | `#!py3 False`         | Enables the Pygments option of a similar name. If set to `#!py True`, will wrap line numbers in `#!html <a>` tags. Used in combination with `linenums` and `line_anchors`. If `line_anchors` is not configured, `__codelineno` will be assumed as the ID prefix.
`line_anchors`            | bool   | `#!py3 False`         | Controls the Pygments option of a similar name. If set to a nonempty string, e.g. `foo`, the formatter will insert an anchor tag with an id (and name) of `foo-<code_block_number>-<line_number>`.
`pygments_lang_class`     | bool   | `#!py3 False`         | If set to True, the language name used will be included as a class attached to the element with the associated `language_prefix`.


## Block
```JavaScript
function() {
  return a +b 
}
```


``` yaml
theme:
  features:
    - content.code.annotate # (1)
```

1.  :man_raising_hand: I'm a code annotation! I can contain `code`, __formatted
    text__, images, ... basically anything that can be written in Markdown.
