# Restaurant Module Boundaries

Restaurant is an optional content module built on top of Core framework contracts, providing restaurant simulation mechanics.

## Module Boundaries

Restaurant depends on Core, but maintains strict isolation from Retail. Menus, culinary blocks, dining orders, and kitchen tasks belong to Restaurant's domain and are not mixed with Retail value catalogs.

## Core Framework Integration

Restaurant consumes Core features including:

- Qualified type IDs and common data models;
- Element definitions and frozen read-only views;
- Customer variants, behavior tasks, and Work Order extensions;
- Server-authoritative state, persistence, and registration lifecycles.

## Development Status

Specific culinary recipes, station blocks, and order mechanics will be specified in future milestones. This page defines architectural boundaries for addon developers.

Compatibility layers should reside in standalone adapters, cleanly disabling features when optional dependencies are absent.
