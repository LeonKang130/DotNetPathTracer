# Week 2 Progress Report

In this week we designed a rendering framework based on that of [LuisaRender](https://github.com/LuisaGroup/LuisaRender) and [pbrt-v3](https://github.com/mmp/pbrt-v3) and implemented a subset of its components in F#, since we considered it to be more concise after our first week's experiments. The renderer is not designed for real-time rendering since it lacks GPU support, but we will still try to implement some of the modern real-time ray tracing techniques.

The repository of the renderer is listed here:

-   [Barnacle](https://github.com/LeonKang130/Barnacle)

Currently we haven't added support for scene I/O, so to run the renderer you need to first clone the repository and then run `dotnet run -c Release`.

In addition to what we have achieved in the first week, we added the following features that were absent in smallpt:

-   Thin-lens camera supporting depth of field
-   Next-event estimation and multiple importance sampling
-   BVH acceleration structure for faster tracing
-   Path-traced direct/global illumination

Here is a sample output from our renderer:

![Sample Depth-of-Field](https://github.com/LeonKang130/DotNetPathTracer/blob/main/Week%202/sample.png)
