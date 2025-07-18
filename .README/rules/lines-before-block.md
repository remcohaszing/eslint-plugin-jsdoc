# `lines-before-block`

This rule enforces minimum number of newlines before JSDoc comment blocks
(except at the beginning of a block or file).

## Options

### `checkBlockStarts`

Whether to additionally check the start of blocks, such as classes or functions.
Defaults to `false`.

### `lines`

The minimum number of lines to require. Defaults to 1.

### `ignoreSameLine`

This option excludes cases where the JSDoc block occurs on the same line as a
preceding code or comment. Defaults to `true`.

### `ignoreSingleLines`

This option excludes cases where the JSDoc block is only one line long.
Defaults to `true`.

### `excludedTags`

An array of tags whose presence in the JSDoc block will prevent the
application of the rule. Defaults to `['type']` (i.e., if `@type` is present,
lines before the block will not be added).

|||
|---|---|
|Context|everywhere|
|Tags|N/A|
|Recommended|false|
|Settings||
|Options|`checkBlockStarts`, `excludedTags`, `ignoreSameLine`, `ignoreSingleLines`, `lines`|

## Failing examples

<!-- assertions-failing linesBeforeBlock -->

## Passing examples

<!-- assertions-passing linesBeforeBlock -->
