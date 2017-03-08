# implementing ray picking in mapboxgl to select extruded polygons

## querying a source

Does the list returned when querying rendered features contain buildings that
are only shown partly in the viewport?

```js
const layers = ['extruded-buildings']
const buildings = map.queryRenderedFeatures({layers})
console.log(buildings) // Yup!
```

## data we might need

1. a single feature's properties:
    - layer:
        - layer id
    - properties:
        - height
    - geometry:
        - polygon (coordinates)
2. a click's coordinates
3. CameraOptions
    - center
    - bearing
    - pitch

## job to be done

- we have a list of geometries with coordinates in geographic space and a height value.
- we have a camera center, bearing and pitch
- we have a coordinate in geographic space of a ray's destination
- first we want to know if the ray intersects with any of the geometries
- then we want to know which of those geometries is the closest to the camera

- we might need vectors & matrices (gl-matrix?)
- we might want to do our math in 3d space (not geographic space)
    - for this use `Map.project(lnglat) -> Point`
-



## construct the ray from the mouse coordinates

- world x,y,z position of the camera (for the origin of the ray)
- Ray
- list of planes ()
-

```js
// Vector
const Vector = {}


// Given a ray (origin and direction), we need to know if it intersect an object on the scene
function trace (ray, scene, depth) {}




```
- geometric intersection testing.
- Compute planes for each side of a polygon's extrusion
- axis-aligned bounding-box


1. projection matrix P
2. camera transform C


---
References:
- [MapboxGL API](https://www.mapbox.com/mapbox-gl-js/api/)
- [Use ray picking to query extrusions in "queryRenderedFeatures"](https://github.com/mapbox/mapbox-gl-js/issues/3122)
- [OpenGL Picking in 3D](http://schabby.de/picking-opengl-ray-tracing/)
- [](http://stackoverflow.com/questions/2093096/implementing-ray-picking#2093149)
- [Vector operations](http://www.macwright.org/literate-raytracer/vector.html)
- [three.js Ray](https://threejs.org/docs/index.html?q=ray#Reference/Math/Ray)
- [Mouse Picking with Raycasting](http://antongerdelan.net/opengl/raycasting.html)
- [gl-matrix](http://glmatrix.net/)
- [Viewing Fustrum (wikipedia)](https://en.wikipedia.org/wiki/Viewing_frustum)