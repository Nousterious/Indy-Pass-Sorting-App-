# Indy Pass Northeast Finder

A single HTML file that ranks every downhill ski area on the [Indy Pass](https://www.indyskipass.com/) in the Northeast by how far it actually is from you, how much vertical it has, and how many lifts turn.

Type a ZIP code. The list re-sorts. Tap an address and your maps app opens with directions already routed.

No build step, no dependencies, no server. Open `index.html` in a browser and it works — including offline, since the ski area data and the full US ZIP code table are embedded in the file.

## What's in it

**42 alpine areas** across NY, CT, MA, VT, NH, plus Maine and New Jersey behind a state filter. Cross-country-only centers are deliberately excluded.

**Sortable on any column** — road miles, drive time, vertical drop, lifts, trails, or name. Click a header twice to reverse it.

**Verified addresses.** Every base-lodge address was checked against the operator's own contact or directions page, then cross-checked against the coordinates used for the distance math. Each one is a tap target that hands off to Google Maps with your ZIP as the origin, plus a copy button for pasting into Apple Maps or Waze.

**Filters** for night skiing and terrain parks.

## About the distance model

The page makes no network calls, so it can't ask a routing service for real driving directions. Distances and times are modelled instead, and it's worth knowing how before you trust a number.

Straight-line distance is measured from the ZIP centroid, then corrected two ways. First, roads wander: short trips detour more than long interstate runs, so the correction factor slides from about 1.35× down to 1.17× as distance grows. Second, average speed climbs with trip length as surface streets give way to highway.

**Water barriers get routed around explicitly.** Long Island has no road east or north — every mainland trip funnels through the Bronx crossings — so a straight line badly understates Connecticut and New England. ZIPs in Kings, Queens, Nassau and Suffolk are routed through the Throgs Neck Bridge before distance is measured. Without that correction, Powder Ridge reads as 70 miles away; the real answer is closer to 103.

Calibrated against nine known routes from western Long Island:

| Destination | Modelled | Actual |
|---|---|---|
| Mohawk Mountain, CT | 104 mi / 2h09 | ~105 mi / ~2h20 |
| Catamount | 121 mi / 2h25 | ~120 mi / ~2h25 |
| Berkshire East | 170 mi / 3h10 | ~165 mi / ~3h05 |
| West Mountain | 209 mi / 3h47 | ~215 mi / ~3h45 |
| Cannon Mountain | 300 mi / 5h15 | ~300 mi / ~5h15 |
| Jay Peak | 341 mi / 5h57 | ~350 mi / ~6h20 |

Times assume free-flowing traffic with no stops or weather, so treat them as a floor rather than a forecast. The model also assumes you drive: the Port Jefferson–Bridgeport and Orient Point–New London ferries can beat these numbers to Connecticut and points east.

Only the continental US is covered, and only the Long Island barrier is modelled. Other origins separated from their destination by water — the islands off Massachusetts, for instance — will read optimistically.

## Data and credits

**ZIP code coordinates** are derived from [GeoNames](https://www.geonames.org), licensed [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Coordinates have been rounded to three decimal places and all fields other than ZIP, latitude, longitude, city and state were removed. Obtained via the [`zipcodes`](https://github.com/seanpianka/zipcodes) package (MIT), which pairs GeoNames coordinates with the public-domain USPS ZIP Locale Detail list.

**Ski area statistics** were compiled from the [Indy Pass East roster](https://www.indyskipass.com/our-resorts/east). **Addresses** were verified individually against each operator's own website.

**Typefaces** — Archivo, Public Sans and IBM Plex Mono — load from Google Fonts and are not redistributed here. All three are SIL OFL 1.1.

Full details in [NOTICE](NOTICE).

## License

Source code is [MIT licensed](LICENSE). The bundled ZIP coordinate data carries its own CC BY 4.0 attribution requirement, described above and in NOTICE — if you fork this and redistribute it, that credit needs to travel with it.

## Disclaimer

Unofficial. Not affiliated with, endorsed by, or sponsored by Indy Pass or any listed resort; their names are used descriptively. Resort statistics, pass partnerships and blackout dates change between seasons — verify with the resort before you drive four hours.
