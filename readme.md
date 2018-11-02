
# Norwegian hiking map

Originally from [svn.openstreetmap.org/applications/rendering/nor-hikingmap](https://svn.openstreetmap.org/applications/rendering/nor-hikingmap/)

Mapnik style sheets that implement conventions as often seen in Norwegian hiking and nordic skiing maps. The separate style sheets for winter and summer feature different colour schemes.

The summer map is a hiking one, including support for these tags:

```
trailblazed=yes (and marked_trail=blue for compatibility)
trail_visibility=* -- indistinct trails are shown with open dashing
tracktype=grade1-2 -- often used on "trillestier"
tracktype=grade3-5 -- tracks from tractors or logging machines
```

The winter map tones down paths and instead shows skiing pistes:

```
piste:type=nordic|downhill
piste:difficulty=*
piste:grooming=*
```

Additionally, hiking related POIs are shown starting at lower zoom levels.
Examples are trailhead parking lots "utfartsparkering"; amenity=parking with hiking=yes, sports chapels; amenity=place_of_worship with hiking=yes, serviced and unlocked cabins and emergency shelters, lean-tos and viewpoints.

The style sheets are modular, simplifying reuse and customization.

Maintained by Vidar Bronken Gundersen (vibrog)

## Cartography and symbols

The cartography featured on these maps takes influence from hiking maps published by Asker Skiklubb (http://asker-skiklubb.no/), which are essentially orienteering maps cleaned up visually, with added POIs, place names and highlighting of skiing tracks and marked hiking trails.

Symbols come courtesy of a standard created by Norwegian mapping authorities, that are now freely available, and used with permission.

  Symbolskrifter for friluftsliv og sport
  [en:Symbol fonts for recreation and sport] (1997). Statens kartverk
  Landkartdivisjonen. ISBN 82-90408-52-8, Retrieved from
  http://www.statkart.no/filestore/Standardisering/docs/symbol.pdf

This standard defines CMYK colour values for symbol classes.
Substituted by the following RGB equivalents:

```
#d0006f (purple) -- activities
#007d33 (green)  -- nature areas
#b21416 (red)    -- culture and entertainment
#007db4 (blue)   -- services and transport
```

## Contours or hillshading

Terrain and elevation is normally shown using contour lines and/or hillshading in hiking maps. Norway is cut short by the fact that the SRTM DEM stops at 60.4° north, which includes "Nordmarka".

viewfinderpanoramas.com and ASTER offer more coverage, but legal restrictions on reuse of these data sets are unclear.

## Installation and usage

The style sheets require Mapnik 0.7.1.

Assume the inc folder from the standard OSM Mapnik style sheet.
It is suggested to create a symlink to a checkout of this.

Import OSM data using an osm2pgsql style file where
`importadditions.osm2pgsql.style` is appended to a checkout of
[svn.openstreetmap.org/applications/utils/export/osm2pgsql/default.style](http://svn.openstreetmap.org/applications/utils/export/osm2pgsql/default.style)

Point your generate_tiles.py script or mod_tile config
to hikingmap.xml and/or pistemap.xml

## TODO

* text: place=locality|farm|isolated_dwelling|island|islet|suburb
* railway=platform or waterway=dam or man_made=pier

* barrier=stile|kissing_gate
* barrier=toll_booth

* piste:type=snow_park (no:terrengpark)
* sport=* symbols from zoom 17

* regional hiking routes network=iwn/nwn/rwn at zoom=10-11
* shooting range types: Clay pigeon, pistol
* piste:oneway=yes
* piste:lit=yes
* [piste:type]='playground' or [leisure]='ski_playground'
