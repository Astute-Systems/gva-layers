# GVA Layers

Example layer configuration branches for **GVA BMS** (Battlespace Management System).

Each branch provides a ready-to-use set of JSON configuration files for a specific demo location.
Use the **GitHub → Sync Layers** panel inside GVA BMS to download and apply a branch.

## Directory Structure

Configuration files are grouped by product, with a lightweight top-level manifest
(`config.json`) pointing at each product's main config file:

```
gva-layers/
├── config.json                          # top-level manifest — points to each product's config file
├── talos/
│   ├── talos_config.json                # main settings — map centre, connectors, pointer to data layers
│   ├── bms-data-layers.json             # data layer definitions — airports, airspaces, maritime zones, etc.
│   ├── bms-map-sources.json             # map tile/source definitions
│   ├── data/                            # local geospatial data referenced by bms-data-layers.json
│   └── connectors/
│       ├── adbs/adsb_config.json        # ADS-B connector config
│       ├── ais/ais_config.json          # AIS connector config
│       ├── cot/cot_config.json          # Cursor-on-Target connector config
│       ├── gtfs/gtfs_sources.json       # GTFS real-time transit sources
│       ├── sapient/sapient_config.json  # Sapient connector config
│       ├── spx/spx_config.json          # SPX connector config
│       └── json/                        # static/recorded JSON object feeds
│           ├── demo_objects.json
│           ├── test_objects.json
│           ├── adsb_recorded_objects.json
│           └── ais_recorded_objects.json
├── hermes/
│   └── hermes-config.json               # Hermes product configuration
└── atlas/
    └── atlas-config.json                # Atlas product configuration (GVA HMI config)
```

| Directory | Purpose |
|-----------|---------|
| `talos/` | Layer configuration files for Talos |
| `atlas/` | Layer configuration files for Atlas |
| `hermes/` | Layer configuration files for Hermes |

## Available Demo Locations

| Branch | Location | Centre |
|--------|----------|--------|
| `london` | Farnborough, UK | 51.2777° N, 0.7761° W |
| `millbrook` | Millbrook Proving Ground (UTAC), Bedford, UK | 52.0433° N, 0.5389° W |
| `paris` | CDG Airport, France | 49.0097° N, 2.5479° E |
| `brisbane` | Fortitude Valley, QLD, AU | 27.4568° S, 153.0357° E |
| `perth` | Perth CBD, WA, AU | 31.9505° S, 115.8605° E |

## Files per Branch

| File | Purpose |
|------|---------|
| `talos/talos_config.json` | Main settings — map centre coordinates, connector config, and pointer to the layers file |
| `talos/bms-data-layers.json` | Data layer definitions — airports, airspaces, maritime zones, etc. |
| `talos/connectors/json/demo_objects.json` | Sample pre-placed military symbols around the demo area |

## Usage

1. Open GVA BMS in standalone mode.
2. Click the **Settings** toolbar button.
3. Select the **GitHub** tab.
4. The repository URL defaults to `https://github.com/Astute-Systems/gva-layers`.
5. Choose a **Demo Location** from the drop-down.
6. Click **Sync Layers** — BMS clones the branch and writes the JSON files locally.
7. Re-launch BMS with the synced settings file:
   ```
   gva-app-bms --settings ~/.local/share/gva-app-bms/gva-layers/talos/talos_config.json
   ```

## Adding a New Location

1. Create a new branch from `main`.
2. Edit `talos/talos_config.json` with the correct default lat/lon and zone name.
3. Edit `talos/bms-data-layers.json` to reference the correct regional data files.
4. Optionally update `talos/connectors/json/demo_objects.json` with representative symbols.
5. Push the branch — it will appear in the BMS branch selector after the next pull.
