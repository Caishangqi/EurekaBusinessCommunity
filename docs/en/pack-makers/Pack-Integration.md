# Modpack Integration & Debugging

This document provides testing guidelines and integration best practices for modpack creators.

## Recommended Integration Workflow

1. Configure a test instance running Minecraft `1.21.1` and NeoForge `21.1.x`;
2. Install EurekaBusiness along with its declared dependencies;
3. Launch the instance once to generate initial configurations, then stop the server before editing catalogs;
4. Validate item recognition, price synchronization, customer purchases, and world persistence on a dedicated server;
5. Package verified configuration files into the distribution profile with version release notes.

## Development Reset Command

The workspace provides the `resetRetailConfig` Gradle task to purge development configurations under `runs/`, regenerating fresh defaults from code seeds:

```text
gradlew resetRetailConfig
```

This task is intended solely for developer testing and should not be invoked as a runtime migration mechanism by players.

## Server Validation Checklist

- Client tooltips and price bands match server catalog snapshots;
- Unregistered items or elements are rejected and do not publish;
- Customers reliably navigate to the lowest-priced pedestal when identical items differ in price;
- Failed transactions never deduct inventory without crediting payments;
- World saves, server restarts, and client reconnections maintain consistent shop and customer states;
- Closing a shop prevents new spawns and gracefully drains existing shoppers.

## Architecture Boundaries

- Do not treat static documentation text as a runtime configuration file;
- Never treat local development assets as a shipping resource or runtime dependency;
- Client-provided prices, quantities, and element lists are untrusted;
- Avoid scanning all shop pedestals or entities per tick. Rely on configuration updates, inventory changes, or server events.
