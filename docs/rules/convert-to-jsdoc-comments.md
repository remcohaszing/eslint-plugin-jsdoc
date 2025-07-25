<a name="user-content-convert-to-jsdoc-comments"></a>
<a name="convert-to-jsdoc-comments"></a>
# <code>convert-to-jsdoc-comments</code>

Converts single line or non-JSDoc, multiline comments into JSDoc comments.

Note that this rule is experimental. As usual with fixers, please confirm
the results before committing.

<a name="user-content-convert-to-jsdoc-comments-options"></a>
<a name="convert-to-jsdoc-comments-options"></a>
## Options

<a name="user-content-convert-to-jsdoc-comments-options-enablefixer"></a>
<a name="convert-to-jsdoc-comments-options-enablefixer"></a>
### <code>enableFixer</code>

Set to `false` to disable fixing.

<a name="user-content-convert-to-jsdoc-comments-options-lineorblockstyle"></a>
<a name="convert-to-jsdoc-comments-options-lineorblockstyle"></a>
### <code>lineOrBlockStyle</code>

What style of comments to which to apply JSDoc conversion.

- `block` - Applies to block-style comments (`/* ... */`)
- `line` - Applies to line-style comments (`// ...`)
- `both` - Applies to both block and line-style comments

Defaults to `both`.

<a name="user-content-convert-to-jsdoc-comments-options-enforcejsdoclinestyle"></a>
<a name="convert-to-jsdoc-comments-options-enforcejsdoclinestyle"></a>
### <code>enforceJsdocLineStyle</code>

What policy to enforce on the conversion of non-JSDoc comments without
line breaks. (Non-JSDoc (mulitline) comments with line breaks will always
be converted to `multi` style JSDoc comments.)

- `multi` - Convert to multi-line style
```js
/**
 * Some text
 */
```
- `single` - Convert to single-line style
```js
/** Some text */
```

Defaults to `multi`.

<a name="user-content-convert-to-jsdoc-comments-options-allowedprefixes"></a>
<a name="convert-to-jsdoc-comments-options-allowedprefixes"></a>
### <code>allowedPrefixes</code>

An array of prefixes to allow at the beginning of a comment.

Defaults to `['@ts-', 'istanbul ', 'c8 ', 'v8 ', 'eslint', 'prettier-']`.

Supplying your own value overrides the defaults.

<a name="user-content-convert-to-jsdoc-comments-options-contexts"></a>
<a name="convert-to-jsdoc-comments-options-contexts"></a>
### <code>contexts</code>

The contexts which will be checked for preceding content.

Defaults to `ArrowFunctionExpression`, `FunctionDeclaration`,
`FunctionExpression`, `TSDeclareFunction`.

<a name="user-content-convert-to-jsdoc-comments-options-contextsafter"></a>
<a name="convert-to-jsdoc-comments-options-contextsafter"></a>
### <code>contextsAfter</code>

The contexts which will be checked for content on the same line after.

Defaults to an empty array.

<a name="user-content-convert-to-jsdoc-comments-options-contextsbeforeandafter"></a>
<a name="convert-to-jsdoc-comments-options-contextsbeforeandafter"></a>
### <code>contextsBeforeAndAfter</code>

The contexts which will be checked for content before and on the same
line after.

Defaults to `VariableDeclarator`, `TSPropertySignature`, `PropertyDefinition`.

|||
|---|---|
|Context|`ArrowFunctionExpression`, `FunctionDeclaration`, `FunctionExpression`|
|Tags|(N/A)|
|Recommended|false|
|Settings|`minLines`, `maxLines`|
|Options|`enableFixer`, `enforceJsdocLineStyle`, `lineOrBlockStyle`, `allowedPrefixes`, `contexts`, `contextsAfter`, `contextsBeforeAndAfter`|

<a name="user-content-convert-to-jsdoc-comments-failing-examples"></a>
<a name="convert-to-jsdoc-comments-failing-examples"></a>
## Failing examples

The following patterns are considered problems:

````ts
// A single line comment
function quux () {}
// "jsdoc/convert-to-jsdoc-comments": ["error"|"warn", {"enforceJsdocLineStyle":"single"}]
// Message: Line comments should be JSDoc-style.

// A single line comment
function quux () {}
// "jsdoc/convert-to-jsdoc-comments": ["error"|"warn", {"contexts":[{"context":"FunctionDeclaration","inlineCommentBlock":true}]}]
// Message: Line comments should be JSDoc-style.

// A single line comment
function quux () {}
// "jsdoc/convert-to-jsdoc-comments": ["error"|"warn", {"enableFixer":false,"enforceJsdocLineStyle":"single"}]
// Message: Line comments should be JSDoc-style.

// A single line comment
function quux () {}
// "jsdoc/convert-to-jsdoc-comments": ["error"|"warn", {"enforceJsdocLineStyle":"single","lineOrBlockStyle":"line"}]
// Message: Line comments should be JSDoc-style.

/* A single line comment */
function quux () {}
// "jsdoc/convert-to-jsdoc-comments": ["error"|"warn", {"enforceJsdocLineStyle":"single"}]
// Message: Block comments should be JSDoc-style.

/* A single line comment */
function quux () {}
// "jsdoc/convert-to-jsdoc-comments": ["error"|"warn", {"enforceJsdocLineStyle":"single","lineOrBlockStyle":"block"}]
// Message: Block comments should be JSDoc-style.

// A single line comment
function quux () {}
// "jsdoc/convert-to-jsdoc-comments": ["error"|"warn", {"enforceJsdocLineStyle":"multi"}]
// Message: Line comments should be JSDoc-style.

// A single line comment
function quux () {}
// Message: Line comments should be JSDoc-style.

/* A single line comment */
function quux () {}
// "jsdoc/convert-to-jsdoc-comments": ["error"|"warn", {"enforceJsdocLineStyle":"multi"}]
// Message: Block comments should be JSDoc-style.

// Single line comment
function quux() {

}
// Settings: {"jsdoc":{"structuredTags":{"see":{"name":false,"required":["name"]}}}}
// Message: Cannot add "name" to `require` with the tag's `name` set to `false`

/* Entity to represent a user in the system. */
@Entity('users', getVal())
export class User {
}
// "jsdoc/convert-to-jsdoc-comments": ["error"|"warn", {"contexts":["ClassDeclaration"]}]
// Message: Block comments should be JSDoc-style.

/* A single line comment */ function quux () {}
// Settings: {"jsdoc":{"maxLines":0,"minLines":0}}
// "jsdoc/convert-to-jsdoc-comments": ["error"|"warn", {"enforceJsdocLineStyle":"single"}]
// Message: Block comments should be JSDoc-style.

var a = []; // Test comment
// "jsdoc/convert-to-jsdoc-comments": ["error"|"warn", {"contextsAfter":["VariableDeclarator"],"contextsBeforeAndAfter":[]}]
// Message: Line comments should be JSDoc-style.

var a = []; // Test comment
// "jsdoc/convert-to-jsdoc-comments": ["error"|"warn", {"contextsAfter":[{"context":"VariableDeclarator","inlineCommentBlock":true}],"contextsBeforeAndAfter":[]}]
// Message: Line comments should be JSDoc-style.

var a = []; // Test comment
// Settings: {"jsdoc":{"maxLines":0,"minLines":0}}
// "jsdoc/convert-to-jsdoc-comments": ["error"|"warn", {"contextsAfter":[{"context":"VariableDeclarator","inlineCommentBlock":true}],"contextsBeforeAndAfter":[]}]
// Message: Line comments should be JSDoc-style.

// Test comment
var a = [];
// "jsdoc/convert-to-jsdoc-comments": ["error"|"warn", {"contextsBeforeAndAfter":["VariableDeclaration"]}]
// Message: Line comments should be JSDoc-style.

var a = []; // Test comment
// "jsdoc/convert-to-jsdoc-comments": ["error"|"warn", {"contextsBeforeAndAfter":["VariableDeclaration"]}]
// Message: Line comments should be JSDoc-style.

interface B {
  g: () => string; // Test comment
}
// "jsdoc/convert-to-jsdoc-comments": ["error"|"warn", {"contextsBeforeAndAfter":["TSPropertySignature"]}]
// Message: Line comments should be JSDoc-style.

class TestClass {
  public Test: (id: number) => string; // Test comment
}
// "jsdoc/convert-to-jsdoc-comments": ["error"|"warn", {"contextsBeforeAndAfter":["PropertyDefinition"]}]
// Message: Line comments should be JSDoc-style.

var a = []; // Test comment
// "jsdoc/convert-to-jsdoc-comments": ["error"|"warn", {"contextsBeforeAndAfter":["VariableDeclarator"]}]
// Message: Line comments should be JSDoc-style.
````



<a name="user-content-convert-to-jsdoc-comments-passing-examples"></a>
<a name="convert-to-jsdoc-comments-passing-examples"></a>
## Passing examples

The following patterns are not considered problems:

````ts
/** A single line comment */
function quux () {}
// "jsdoc/convert-to-jsdoc-comments": ["error"|"warn", {"enforceJsdocLineStyle":"single"}]

/** A single line comment */
function quux () {}
// "jsdoc/convert-to-jsdoc-comments": ["error"|"warn", {"enforceJsdocLineStyle":"multi"}]

/** A single line comment */
function quux () {}
// "jsdoc/convert-to-jsdoc-comments": ["error"|"warn", {"lineOrBlockStyle":"line"}]

/** A single line comment */
function quux () {}
// "jsdoc/convert-to-jsdoc-comments": ["error"|"warn", {"lineOrBlockStyle":"block"}]

/* A single line comment */
function quux () {}
// "jsdoc/convert-to-jsdoc-comments": ["error"|"warn", {"enforceJsdocLineStyle":"single","lineOrBlockStyle":"line"}]

// A single line comment
function quux () {}
// "jsdoc/convert-to-jsdoc-comments": ["error"|"warn", {"enforceJsdocLineStyle":"single","lineOrBlockStyle":"block"}]

// @ts-expect-error
function quux () {}

// @custom-something
function quux () {}
// "jsdoc/convert-to-jsdoc-comments": ["error"|"warn", {"allowedPrefixes":["@custom-"]}]

// Test comment
var a = [];
// "jsdoc/convert-to-jsdoc-comments": ["error"|"warn", {"contextsAfter":["VariableDeclarator"],"contextsBeforeAndAfter":[]}]
````

