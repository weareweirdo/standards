# HTML Guidelines

## General formatting

- Paragraphs of text should always be placed in a <p> tag. Never use multiple <br> tags.
- Items in list form should always be in <ul>, <ol>, or <dl>. Never use a set of <div> or <p>.
- Every form input that has text attached should utilize a <label> tag. Don't replace <label> with just a placeholder. [Here's how to do it](https://a11yproject.com/posts/placeholder-input-elements/).

## Layout

We often try to combine a few classes, each with different purposes together on a single element. For example, combining layout and component specific styles:

```
<div class="grid my-component">
    <div class="grid__item one-third--medium my-component__item">
        ...
    </div>
</div>
```

This kind of mixing of concerns often leads to bugs and un-predicable behaviour. Introduce additional elements, creating buffers between different types of styles. The above example would now look something like this:

```
<div class="my-component">
    <div class="grid">
        <div class="grid_item one-third--medium">
            <div class="my-component__item">
                ...
            </div>
        </div>
    </div>
</div>
```