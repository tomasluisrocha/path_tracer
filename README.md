# Ray Tracer in C++

A CPU path tracer written in C++, following [*Ray Tracing in One Weekend*](https://raytracing.github.io/books/RayTracingInOneWeekend.html) and [*Ray Tracing: The Next Week*](https://raytracing.github.io/books/RayTracingTheNextWeek.html) by Peter Shirley, Trevor David Black, and Steve Hollasch.

![Render](renders/image_final.png)

## Features

- Path tracing with a configurable bounce depth
- Antialiasing with jittered sub-pixel sampling
- Lambertian and metal (adjustable fuzz) materials
- Gamma correction
- Positionable camera with adjustable field of view
- Depth of field (defocus blur)
- Motion blur (moving spheres, rays sampled at random times)
- Bounding volume hierarchy (BVH) built from axis-aligned bounding boxes
- Textures: solid color, 3D checker, and image textures with sphere UV mapping
- PPM image output

## Build and run

```bash
g++ -O3 -o raytracer main.cc
./raytracer > image.ppm
```

Image textures are loaded with [stb_image](https://github.com/nothings/stb), a single-header library.
Run the program from the directory containing `earthmap.jpg` for the earth scene.

## Scenes

Scenes are separate functions in `main.cc`, selected by the `switch` in `main()`:

| # | Scene |
| --- | --- |
| 1 | Bouncing spheres (motion blur, BVH) |
| 2 | Checkered spheres |
| 3 | Earth (image texture) |

## Configuration

The scene and camera are set in `main.cc`:

```cpp
cam.aspect_ratio      = 16.0 / 9.0;
cam.image_width       = 400;
cam.samples_per_pixel = 100;
cam.max_depth         = 50;

cam.vfov     = 20;
cam.lookfrom = point3(13, 2, 3);
cam.lookat   = point3(0, 0, 0);
cam.vup      = vec3(0, 1, 0);

cam.defocus_angle = 0.6;   // 0 = no blur
cam.focus_dist    = 10.0;  // distance to the plane of perfect focus
```

## Credits

Based on *Ray Tracing in One Weekend* and *Ray Tracing: The Next Week* (<https://raytracing.github.io/>), released under CC0.