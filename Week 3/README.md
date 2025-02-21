# README

In this week we refactored our project [Barnacle](https://github.com/LeonKang130/Barnacle), putting shared data structures and algorithms into a new directory and namespace, and added a new integrator `PSSMLT`, which implements the "Primary Sample Space Metropolis Light Transport" algorithm by Kelemen et al. (the paper can be found [here](https://cg.iit.bme.hu/%7Eszirmay/paper50_electronic.pdf)).

Here is a sample image rendered using this algorithm:

![PSSMLT](sample.png)

PSSMLT employs a very different approach from our previous path tracer implementation, that although it shares almost the same tracing function as our `PathTracingIntegrator`, it instead performs Metropolis-Hastings over the space of the random number sequence (primary samples) used to generate samples in the path space. While implementations of this algorithm on the CPU tends to store these samples in an `std::vector` and ones on the GPU tends to allocate dedicated buffers for them, we instead chose to use `Unsafe.stackalloc` to temporarily store these samples on the runtime stack instead of on the heap using `Array` or `ResizeArray` so that we can avoid adding stress to the garbage collector. Details of this part can be found in `Extensions/Integrator/PSSMLT.fs`.

 Although F# can be written in an imperative style for optimal performance, the lack of `unsafe` blocks is one thing making coding in F# greatly different from in C#.

Under the same time budget, PSSMLT usually generates images with slightly more noise than path tracing does. However, it does appear to be superior when the visibility in the scene is difficult due to its nature of exploration in the path space by extending its Markov chains.
