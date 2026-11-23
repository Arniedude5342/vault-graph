---
type: reference
summary: Snippets that show how the parser ignores links, tags and tasks inside code.
---
# Code Examples

Inline code such as `[[Not A Link]]` and `#not-a-tag` is ignored. A real link: [[Home]].

```markdown
# Not a heading
- [ ] Not a task
[[Also Not A Link]]
```

~~~
- [ ] Still not a task
~~~

## After the fences
- [ ] A real task after the code blocks
