# Monte Carlo Geometry Processing (6/23, 3:30PM)

## PDEs
- Laplacian: implicitly describe in terms of derivatives. 
- Traditional method for solving PDEs use finite dimensional approximation <- can be difficult 
    - We will have numerical errors
    - Geometry in the real world is complex and takes time to mesh
    - Meshing cannot be parallelized easily
    - Needs lot of manual clean up since most geometry is complex
    - Bad mesh can yield a false impression of reality
So if mesh is slow, who cares for fast solvers?
- Most pipelines today are bottleneck because of this
- The point of research might be to look at faster meshing
We MUST find ways to handle greater geometrical complexity
- Early days, we would use finite element radiosity
    - Robust meshing was hard so idea became slow
- Now, we use Monte Carlo methods
    - Avoids meshing
    - Repeated random sampling
    - Ray-scene
    - We aggregate results from N samples to obtain the final output
    - Can handle immense geometric complexity
    - Works with any scene you ask it to do

How can we make simulation described by laplacian PDEs like Monte Carlo rendering?
- Helps us with illumination rendering
- Ray tracing to random walks to solve Laplace PDEs
- Meshing is hard, finding closest point is easy
- We can analyze locally
- Makes thermal analysis easier since meshing is not really there
- Monte Carlo solvers are discretization-free

## BASICS of MONTE CARLO
- Special type of algorithms to use repeated random sampling to obtain approx solutions to difficult computational problems
- Can be used for simulation, integration, sampling, and optimization
- Not all randomized algorithms are Monte Carlo
- Motivation
    - Some problems cannot be numerically measured trivially
- Solution is approximate but correct eventually
- Monte Carlo is easy to parallelize
Why integration?
- Most times analytic integration are not useful
- We have to use numerical methods
- We use quadrature
- Nyquist-shannon ehm says we are to sample as long it is adapted to the high frequency
- Aliasing found in nature
- IDEA: replaace deterministic sample points with random ones
How do we check correctness?
- Monte Carlo estimator is a random variable so the unbiased estimator is correct on average
Numerical and computational issues
- Floating point mishandling
- Expensive integrands may not be parallelized
- Practical obstacles may motivate changes to math foundations
  
Walk on Sphere for Laplace equation
- 
