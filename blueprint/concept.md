# Anteater — Concept Document

*Last major revision: 2026-09-15 (initial version)*

Anteater is a personal, local-first tool for archiving web pages so they remain available to read and semantically search later, independent of whether the original source changes or disappears.

## Problem

- Bookmarking or otherwise just collecting links to pages of interest offers no guarantee that the underlying content stays unchanged, or even stays available at all — pages get edited, moved, or removed over time.
- General-purpose web archiving tools (e.g. archive.is, the Internet Archive's Wayback Machine) address content preservation to some degree, but they save snapshots into a shared, public archive rather than a personal, private collection, and they provide no way to semantically search or analyse what's been archived.
- Making a growing personal collection of pages semantically searchable and analysable isn't straightforward or scalable on its own: simply handing a list of URLs to an agent to fetch and read on demand doesn't provide a clean, reliable, or efficient way to search or reason over the collection as it grows.

## Solution

- Anteater extracts and permanently stores the full content of pages the user chooses to archive, so the archived copy remains available and unchanged regardless of what happens to the original source afterward.
- It allows the user to create personal collections of archived pages that can be semantically searched and analysed.
- The extracted content is processed and indexed in a way that makes it semantically searchable and analysable at scale, so the growing archive can be queried and reasoned over reliably, rather than relying on fetching and reading pages on demand.

<!-- ## Goals -->

<!-- ## Non-Goals -->

<!-- ## Principles -->

<!-- ## Core Concepts -->

<!-- ## High-Level Architecture -->

## Revision History

- 2026-09-15: Initial version
