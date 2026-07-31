# XDG Mapping for Home

Inspired by XDG user dirs, these map object classes to canonical locations.

## Canonical Locations

| XDG Name | Description | Object Classes |
|----------|-------------|----------------|
| `XDG_HOME_KEYS` | Keys, wallet, small essentials | keys, wallet, id_cards |
| `XDG_HOME_SHOES` | Shoes, slippers | shoes, slippers, sandals |
| `XDG_HOME_LAUNDRY_DIRTY` | Dirty clothes hamper | clothes_dirty, towels_dirty |
| `XDG_HOME_LAUNDRY_CLEAN` | Folded/stowed clothes | clothes_clean, towels_clean |
| `XDG_HOME_DISHES_DIRTY` | Sink/rack for dirty dishes | dishes_dirty, utensils_dirty |
| `XDG_HOME_DISHES_CLEAN` | Cupboard/dry rack | dishes_clean, utensils_clean |
| `XDG_HOME_MAIL` | Incoming mail, parcels | mail, packages, letters |
| `XDG_HOME_TOYS` | Kids' toys bin | toys, game_pieces |
| `XDG_HOME_TOOLS` | Household tools | tools, hardware |
| `XDG_HOME_SPORTS` | Sports gear | sports_gear, gym_bag |
| `XDG_HOME_TOILET_PAPER` | Toilet paper storage | toilet_paper_rolls |
| `XDG_HOME_SOAP` | Soap storage | soap_bars, soap_refills |
| `XDG_HOME_BIN` | Waste bin | trash, recyclables |

## Usage

Each `canonical_location` in the `HomeState` schema maps to one of these XDG names. Robots use these to know where objects belong.
