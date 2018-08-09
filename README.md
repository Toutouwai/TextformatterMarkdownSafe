# Markdown Safe

Textformatter module for ProcessWire that simply applies [$sanitizer->entitiesMarkdown()](https://processwire.com/api/ref/sanitizer/entities-markdown/).

## Why?

The advantage over TextformatterMarkdownExtra is that only safe HTML tags are allowed, so you can hook `Fieldtype::markupValue` and if TextformatterMarkdownSafe is applied you can allow HTML markup in the markup value. This, for instance, allows the safe HTML tags to be rendered in Lister columns.

```php
$wire->addHookAfter('Fieldtype::markupValue', function(HookEvent $event) {
    $field = $event->arguments(1);
    $value = $event->arguments(2);
    // Only if TextformatterMarkdownSafe is applied
    if(!in_array('TextformatterMarkdownSafe', $field->textformatters)) return;
    // Allow unencoded HTML tags in markup value
    $event->return = $value;
});
```
