# TTP Monitor

A lightweight TypeScript tool for monitoring Trusted Traveler Program (TTP) / Global Entry appointment availability. It provides a visual grid of available slots and supports specialized checks like weekend-only availability.

## Features

- **Visual Availability Grid**: Shows slots grouped by hour (08:00 - 17:00) and date.
- **Color-Coded Proximity**: Dates are colored based on how soon they occur (Green < 28 days, Yellow < 56 days, Red > 56 days).
- **Weekend Mode**: Specific check for weekend slots within the next 30 days.
- **Custom Time Ranges**: Monitor specific dates beyond the default 6-month window.

## Prerequisites

- [Bun](https://bun.sh/) runtime installed.

## Installation

No installation required besides Bun. Just clone the repository and run the script directly.

## Usage

### Default Run
Checks for available appointments from now until 6 months in the future.
```bash
bun monitor.ts
```

### Custom Date Range
Specify start and end timestamps (ISO 8601 format without milliseconds).
```bash
bun monitor.ts 2024-01-01T00:00:00 2024-06-01T23:59:59
```

### Weekend Check
Look specifically for weekend slots within the next 30 days.
```bash
bun monitor.ts --check-weekends
```

## Configuration

The script contains several configurable options at the top of `monitor.ts`.

### Configurable Options

| Constant | Description | Default |
| :--- | :--- | :--- |
| `LOCATION_ID` | The ID of the TTP enrollment center to monitor. | `5020` (Blaine) |
| `LOCATION_URL` | Information URL for the specific enrollment center. | Blaine NEXUS/FAST |
| `SCHEDULING_URL` | The direct URL to the TTP scheduler for convenience. | TTP Scheduler |

### Grid Visualization Range

You can also adjust the visualization hours by modifying the following constants inside the `main` function:

| Constant | Description | Default |
| :--- | :--- | :--- |
| `minHour` | The start hour for the availability grid (24h format). | `8` (08:00) |
| `maxHour` | The end hour for the availability grid (24h format). | `17` (17:00) |

```typescript
// Example Configuration in monitor.ts
const LOCATION_ID = 5020;
const minHour = 8;
const maxHour = 17;
```

## Example Output

```text
Found 15 slots across 3 days.

=== January 2024 ===
Day        | 08 09 10 11 12 13 14 15 16 17 | Total
-----------+-------------------------------+-------
15 (Mon)   |  .  .  2  1  .  .  .  .  .  . |     3
16 (Tue)   |  .  .  .  .  .  5  2  .  .  . |     7
20 (Sat)   |  1  2  .  .  .  .  .  .  2  . |     5
```

## Development

This entire application was programmed using Google Antigravity.

## License
MIT
