# Week 1 Progress Report

In this week we implemented a classic minimal example of path tracer ([smallpt](http://www.kevinbeason.com/smallpt/)) using C# and F# to learn about the syntax of each of these two .NET languages and to explore their differences in the sense of expressiveness and performance. We modified the code for optimization while keeping the two implementations as equivalent as possible so that we can use them for benchmarking.

Because these implementations are independent .NET projects, we used separate GitHub repositories for each of them to maintain better organization. The repos containing the two implementations are listed here:

-   [smallpt-csharp](https://github.com/LeonKang130/smallpt-csharp)
-   [smallpt-fsharp](https://github.com/LeonKang130/smallpt-fsharp)

To run either of these two, you need to first clone the repository and then run the following command:

```powershell
dotnet run -c Release [samples]
```

By default `samples` is set to 64, in which case $4\times64=256$ ray samples will be taken for each pixel. The result will be output as `image.ppm`. Here is the result we obtained by running the F# implementation with `samples=64`:

![F# implementation output](https://github.com/LeonKang130/DotNetPathTracer/blob/main/Week%201/sample%20-%20fsharp.png)

In addition to implementing smallpt using these two .NET languages, we used [BenchmarkDotNet](https://benchmarkdotnet.org/) to measure the performance of our implementation. Here we focused on the `radiance` function which evaluates the radiance collected along a particular ray (position and direction) and the `renderRow` function which invokes the `radiance` function to evaluate the pixel color for a single row in the final image. We performed our benchmarking on a Laptop(i7-9750H 6 cores), measuring the time consumed and memory allocated with specific row index `y` and samples count `samples` provided to the application. Here are the plots of our benchmarking results:

![RenderRow 192](https://github.com/LeonKang130/DotNetPathTracer/blob/main/Week%201/benchmark%20result%20-%20renderRow%20192.png)



![RenderRow 576](https://github.com/LeonKang130/DotNetPathTracer/blob/main/Week%201/benchmark%20result%20-%20renderRow%20576.png)

Even though F# features extensive support for functional programming and has a very different syntax compared to C#, these differences did not seem to cause much speed penalty or memory overhead as we had expected.
