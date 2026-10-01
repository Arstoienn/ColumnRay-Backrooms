# ColumnRay Backrooms

The Backrooms, Level 0, as a map for [ColumnRay](https://github.com/Arstoienn/ColumnRay), a 2.5D
raycasting engine in plain Java: 86 by 25 metres of yellow wallpaper, carpet and ceiling tiles,
lit by fifty-four fluorescent panels - a few of which are not well.

![An empty room under a row of ceiling panels](images/room.jpg)

![Arches between two rooms](images/arches.jpg)

## Running it

From a checkout of the engine, where this repository is the submodule `maps/backrooms`:

```bash
git submodule update --init maps/backrooms
./run.sh maps/backrooms/backrooms.json --hdr --play
```

The first run bakes the light, which takes about a minute; after that it is read from the cache in
under a second.

## What is in it

| | |
|---|---|
| `backrooms.json` | The map: 31,864 shapes, 54 lights, and the flicker groups |
| `img/` | The surfaces' images, one per material of the source model |
| `images/` | The pictures in this README |

Three of the lamps stutter every so often and one has gone out. Each is a flicker group: the bake lights
it on its own, and the engine adds it back at its level every frame, so a lamp that drops out takes
its share of the bounced light and its own panel's glow with it. A light joins a group with
`"flicker": "name"`, and the map's lighting says how the group behaves:

```json
"flicker": { "pair": { "pattern": "buzz", "every": 15 }, "gone": { "pattern": "dead" } }
```

## How it was made

The source model is unlit: every surface's image is its colour with the author's lighting already
baked into it. ColumnRay bakes its own light, so the images could not be used as they were, or the
light would be counted twice. The wallpaper, carpet and ceiling images were reduced to one colour and
their fine pattern, which takes the pools of light and the shadows out while keeping the texture;
the furniture, doors, windows and fittings keep their images. The light comes from a lamp under each
ceiling panel, and the panels glow.

The geometry was converted face by face: each flat quad with a straight texture became one shape, and
anything else its triangles. Smoke detectors and wall sockets were left out, being thousands of
triangles a few pixels across. The images were brought down to 2048 pixels.

## Source and licence

This work is based on ["Backrooms VR"](https://sketchfab.com/3d-models/backrooms-vr-d9b98eca8d064d0eafcd7f5484bb61ed)
by [carlcapu9](https://sketchfab.com/carlcapu9), licensed under
[CC BY 4.0](http://creativecommons.org/licenses/by/4.0/). It has been changed as described above.

This map is licensed under the same terms, [CC BY 4.0](LICENSE): share and adapt it for any purpose,
crediting carlcapu9 for the original model and this repository for the conversion, as
[NOTICE.md](NOTICE.md) sets out. The engine is separately MIT-licensed.
