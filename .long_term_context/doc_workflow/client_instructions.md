## Code Snippets Workflow

Never write inline code snippets in documentation. Instead, use examples from the SDK example directories and generate embeddable snippets with `frontend/snippets/generate.py`.

Also read and follow the workflow in `.cursor/rules/docs-snippet-workflow.mdc` when updating/creating code snippets.

## Documentation Scope for SDK Features

When documenting new SDK features (especially DurableContext methods and similar core functionality), always create both:

1. **API reference documentation** in the SDK reference pages (`/reference/python/`, `/reference/typescript/`, etc.)
2. **A conceptual guide page** in the appropriate `/v1/` section with:
   - When to use the feature (use cases table)
   - How it works (with diagrams if helpful)
   - Practical examples using SDK snippets
   - Best practices

API reference alone is not sufficient. Users expect guide pages with context and examples. Follow the pattern of existing guide pages like `sleep.mdx` and `events.mdx` in the Durable Workflows section.

## Redirect Handling

When adding or modifying redirects in `next.config.mjs`:

1. **Verify wildcard redirect destinations**: Wildcard redirects like `/guides/:path*` → `/cookbooks/:path*` will 404 if the destination path doesn't exist. Always add explicit redirects for specific paths that would otherwise be caught by wildcards but land on non-existent pages.

2. **Avoid two-hop redirect chains**: When a path redirects via a wildcard to an intermediate destination that then needs another redirect, add a direct redirect from the original source to the final destination. For example, if `/guides/event-driven` → `/cookbooks/event-driven` (via wildcard) and `/cookbooks/event-driven` → `/v1/external-events/run-on-event`, add an explicit redirect from `/guides/event-driven` directly to `/v1/external-events/run-on-event`.

3. **Order matters**: Place explicit redirects before wildcard redirects to ensure specific paths are handled correctly.