# ADR-0001: Page Deletion Model

**Status:** Proposed

## Decision

Page deletion works via a single, uniform mechanism: one "delete everywhere" operation that removes a page's data from all storage layers (for example a database, vector embeddings, and blob storage for HTML/images), used identically whether invoked seconds after archiving (e.g. because after seeing the archived and rendered page, the user decides to not archive this page) or months or years later (e.g. for a general cleanup). There is no separate "staging" or "not yet committed" state and no grace period — every archived page is immediately and fully persisted, and can be deleted at any time through the same operation.

## Alternatives

- **Automatic persist after grace period:** a newly archived page sits in a temporary staging area; after a grace period (or an implicit trigger, e.g. navigating away from the reading view), it's automatically persisted to permanent storage unless explicitly discarded during that window. Rejected: the grace period is inherently arbitrary and ambiguous — how long is long enough, and what exactly counts as "done reading" (switching apps, reading slowly, closing the app) is unclear and would need its own special-casing.
- **Explicit persist required:** a newly archived page sits in a temporary staging area indefinitely and only becomes permanent when the user takes an explicit "keep"/"save" action; without it, the page never gets committed. Rejected: adds friction to the common case, since the vast majority of archived pages are ones the user wants to keep, and unconfirmed staged pages need their own separate lifecycle/cleanup handling for whatever never gets explicitly confirmed.

Both variants share a deeper rejection reason: the robust "delete everywhere" operation has to be built regardless, to support cleanup of pages kept for a long time, so maintaining a second, separate code path (a trivial discard-from-staging path, alongside the coordinated-delete-everywhere path) for what is ultimately the same user-facing action increases the surface area for bugs rather than reducing it, and introduces a confusing intermediate "is this actually saved yet?" state into the app.
