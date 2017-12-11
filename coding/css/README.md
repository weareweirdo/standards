# CSS Guidelines

## Syntax and formatting
- two (2) space indents, no tabs
- 80 character wide columns
- meaningful use of whitespace

### Titling

Begin every new major section of a CSS project with a title:

```
/* ==========================================================================
   #SECTION-TITLE
   ========================================================================== */

.selector { }
```

The title of the section is prefixed with a hash (#) symbol to allow us to perform more targeted searches (e.g. grep, etc.): instead of searching for just SECTION-TITLE—which may yield many results—a more scoped search of #SECTION-TITLE should return only the section in question.

### Anatomy of a ruleset
- related selectors on the same line; - unrelated selectors on new lines
- a space before our opening brace (`{`)
- properties and values on the same line
- a space after our property–value delimiting colon (`:`)
- each declaration on its own new line
- the opening brace (`{`) on the same line as our last selector
- our first declaration on a new line after our opening brace (`{`)
- our closing brace (`}`) on its own new line
- each declaration indented by two (2) spaces
- a trailing semi-colon (`;`) on our last declaration.

Example:

```
.foo, .foo--bar,
.baz {
  display: block;
  background-color: green;
  color: red;
}
```

## Commenting

As a rule, you should comment anything that isn’t immediately obvious from the code alone. That is to say, there is no need to tell someone that color: red; will make something red, but if you’re using overflow: hidden; to clear floats—as opposed to clipping an element’s overflow—this is probably something worth documenting.

### High level

For large comments that document entire sections or components, we use a DocBlock-esque multi-line comment which adheres to our 80 column width. Example:

```
/**
 * The site’s main page-head can have two different states:
 *
 * 1) Regular page-head with no backgrounds or extra treatments; it just
 *    contains the logo and nav.
 * 2) A masthead that has a fluid-height (becoming fixed after a certain point)
 *    which has a large background image, and some supporting text.
 *
 * The regular page-head is incredibly simple, but the masthead version has some
 * slightly intermingled dependency with the wrapper that lives inside it.
 */
```

### Low level
Oftentimes we want to comment on specific declarations (i.e. lines) in a ruleset. To do this we use a kind of reverse footnote:

```
/**
 * Large site headers act more like mastheads. They have a faux-fluid-height
 * which is controlled by the wrapping element inside it.
 *
 * 1. Mastheads will typically have dark backgrounds, so we need to make sure
 *    the contrast is okay. This value is subject to change as the background
 *    image changes.
 */

.page-head--masthead {
  color: $color-masthead; /* [1] */
}
```

### Comments in production

It should go without saying that no comments should make their way into production environments—all CSS should be minified, resulting in loss of comments, before being deployed.

## Naming conventions

### Hyphens
All strings in classes are delimited with a hyphen (`-`), like so:

```
.page-head { }

.sub-content { }
```

Camel case and underscores are not used for regular classes; the following are incorrect:

```
.pageHead { }

.sub_content { }
```
### BEM

BEM splits components’ classes into three groups:

- Block: The sole root of the component.
- Element: A component part of the Block.
- Modifier: A variant or extension of the Block.

```
.person { }
.person__head { }
.person--tall { }
```

Elements are delimited with two (2) underscores (`__`), and Modifiers are delimited by two (2) hyphens (`--`).

Here we can see that `.person {}` is the Block; it is the sole root of a discrete entity. `.person__head {}` is an Element; it is a smaller part of the .person {} Block. Finally, `.person--tall {}` is a Modifier; it is a specific variant of the `.person {}` Block.

### A word on adding more layers

If we were to add another Element—called, let’s say, `.person__eye {}`—to this `.person {}` component, we would not need to step through every layer of the DOM. That is to say, the correct notation would be `.person__eye {}`, and not `.person__head__eye {}`. Your classes do not reflect the full paper-trail of the DOM.

### Modifying elements

Things can get more complex, however. Please excuse the crude analogy, and let’s imagine we have a face Element that is handsome. The person themselves isn’t that handsome, so we modify the face Element directly—a handsome face on a regular person:

```
.person__face--handsome { }
```

But what if that person is handsome, and we want to style their face because of that fact? A regular face on a handsome person:

```
.person--handsome .person__face { }
```

### Namespaces

A naming convention tells us how classes within a component relate to one another, but a namespace will tell us exactly how classes behave in a more global sense. A namespace tells us exactly what a class (or suite of classes) does in non-relative terms:

- **o-:** Signify that something is an Object, and that it may be used in any number of unrelated contexts to the one you can currently see it in. Making modifications to these types of class could potentially have knock-on effects in a lot of other unrelated places. Tread carefully.
- **c-:** Signify that something is a Component. This is a concrete, implementation-specific piece of UI. All of the changes you make to its styles should be detectable in the context you’re currently looking at. Modifying these styles should be safe and have no side effects.
- **u-:** Signify that this class is a Utility class. It has a very specific role (often providing only one declaration) and should not be bound onto or changed. It can be reused and is not tied to any specific piece of UI. You will probably recognise this namespace from libraries and methodologies like SUIT.
- **t-:** Signify that a class is responsible for adding a Theme to a view. It lets us know that UI Components’ current cosmetic appearance may be due to the presence of a theme.
- **s-:** Signify that a class creates a new styling context or Scope. Similar to a Theme, but not necessarily cosmetic, these should be used sparingly—they can be open to abuse and lead to poor CSS if not used wisely.
- **is-, has-:** Signify that the piece of UI in question is currently styled a certain way because of a state or condition. This stateful namespace is gorgeous, and comes from SMACSS. It tells us that the DOM currently has a temporary, optional, or short-lived style applied to it due to a certain state being invoked.
- **_:** Signify that this class is the worst of the worst—a hack! Sometimes, although incredibly rarely, we need to add a class in our markup in order to force something to work. If we do this, we need to let others know that this class is less than ideal, and hopefully temporary (i.e. do not bind onto this).
- **js-:** Signify that this piece of the DOM has some behaviour acting upon it, and that JavaScript binds onto it to provide that behaviour. If you’re not a developer working with JavaScript, leave these well alone.