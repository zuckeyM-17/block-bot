# cad/ — CAD source and STL output

Parametric source for the voxel cube set, plus eventual SO-ARM101 improvements.

## Status

Empty. See [#5 Tinkercad: 3cm stud cube v0](https://github.com/zuckeyM-17/block-bot/issues/5) and [#6 OpenSCAD: parametric cube generator](https://github.com/zuckeyM-17/block-bot/issues/6).

## Layout (planned)

- `cubes/` — `.scad` parametric cube source, exported `.stl` per size/variant.
- `so-arm101-mods/` — improved STLs derived from upstream (Apache-2.0).

## Render

```sh
openscad -o cubes/cube-30.stl cubes/cube.scad -D 'size=30'
```
