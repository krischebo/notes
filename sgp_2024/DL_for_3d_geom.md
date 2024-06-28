# Deep learning for 3D geometry (6/22,11AM)

## PART 1: using NN to solve prediction problems involving 3D geometry

Deep learning = function approx

Characterization of problems
- Type of prediction
- How we represent the data
- What is architecture
- What is the optimization algorithm

Type of prediction, I.e., what is the function 
- We can split into analysis or synthesis
    - analysis: compute some property of existing geometry
    - synthesis: create new geometry
- Analysis
    - Global: take geometry and convert it into a single value to represent it
        - application: classification. Output is a distribution of what the object might be
        - Canonicalization: you have many shapes of the same class but you want to output the transformation such that when you put the input shape through it, you get a uniform output
        - Captioning: output a text string of the input image
    - local: to make it into a point wise signal for representation
        - application: segmentation: you have an input shape and function assigns a value to each point of the shape. It can identify body parts and so on
        - Normal est.: you have cloud points and gives us what direction that may be
        - Geodesic distance: input is a shape and a point on the shape and the output is a field of distances across the surface which will tell us the distance of the path from the original point that is the shortest
        - Shape correspondence: input is two shapes. Output is continuous field of values across the shape which gives us color coded structural correspondence among the two shapes. So same color means thet part is structurally similar in the two shapes
- Synthesis
    - Unconditional: generate a shape from random numbers and it spits out some shapes
        - Noteworthy examples
            - IM Net
            - Wave domain diffusion
            - Mesh GPT: synthesizing geometry, creates vertices and builds off of that. Creates meshes.
    - conditional: input is random numbers with some guidance on how to create the shape
        - Points -> surface; ConvONets & DeepMLS
        - Image -> shape; we might not know the flipside of an image so generating a shape is difficult. NNs can come in here and use previous KB
    - Text -> shape;

Representing data: it is good to have many
- Language processing: tokenizaroin
- Image processing: grid of pixels
- 3D geometry?
    - Meshes: most common-> lots of data. They explicitly represent an object; good for intrinsic analysis.
        - MeshCNN
            - Key idea: define a convolution operator on mesh edges.
            - Can segment body parts or subparts of larger objects
        - DiffusionNet: uses solution of heat equation rather than discrete convolution.
        - MeshGPT
    - Implicit surfaces/ SDFs (similar to Voxels)
    - Voxels (represented as grids, could be similar to implicit surfaces); like 3D grids. Can straightforwardly extend methods from image processing. 
    - Point clouds: very easy to acquire using depth sensor and so on. Good for AI agents making decisions. Using learning to convert point clouds.
        - PointNet: point cloud architecture. Start with nx3 matrix, each point is independently by MLPs. You obtain another matrix of larger size and then more MLPs. 
            - Key idea: individually process each point into a higher dimensional feature space then combine per-point features via an order-invariant function (like max) to get a global feature. Order invariance is important because point clouds are not ordered. 
        - You can segment using these ideas
    - NNs
    - Procedural descriptions 
        - BREPS (produced by CAD using procedures)
        - CAD Reps: infinite-resolution. No loss of quality. Natural choice for using learning within CAD-based models
    - images: multiple views of an object. Can exploit methods of 2D images/vision. 

What architecture? Geometry representation & network architecture are tightly coupled.
- Depp NN: composition of functions (or layers) 
- Some have parameters/weights; called learnable layers; three types:
    - Fully connected/ linear layers (should be called affine): y = Wx+b. Called fully-conn because y is relaeed to every x linearly. When you compose them with non-parameter functions it is called multilayer perception— MLP.
    - Something like convolution: think of inputs and outputs as sets and not vectors which exists in a space. We can think of them spatially and define a local neighborhood. Each output y_i is a fnctn of local neighborhood N of the corresponding element of the input x_i. Often times, function is weighted combination of local neighborhood. Exception is message passing NN. 
    - Attention (transformers): the output is a weighted combination of every input— no localization. Each element of input is transformed into query, key, and value vectors. the weights represents how much “attention” each element pays to each other element (based on distance)
- Gradients

## PART 2: using NN as a representation of 3D geometry/ Neural implicit shape representation

Implicit surfaces:
- CSG (constructive solid geometry): objects are properly defined in terms of inside and outside the objects. Inside points are negatives and outside are positive so set operations are easy to perform. Max gives intersection and min gives union.
- Taxonomy: 
    - Signed distance (SDFs): encodes distance to closest point on surface. 
    - Conservative SDFs (approx SDFs): we require the absolute value of the function to be less than the distance to the closest point on the surface.
- Surface extraction
    - Marching cubes: identify voxels with surface present and draw surface in each of these voxels.
        - Using distance info for SDF case: sellan et al, 2023
        - Chen et al 2023
- Implicit vs explicit
    - Implicit: answer questions about points in space. In implicit representations, topologyy changes are constant. To of to explicit use marching cubes.
    - explicit: answer questions about surface itself. Faster and what we generally want. To go to implicit, we use distance computation.

Digital representations
- Analytical: f(x,y)=x2+y2-r2. Slow to compute complex formulas and cannot always find analytical representation
- grid: they do not scale well; solution is adaptive grids. 
    - Think of them as functions: mapping a point in our domain to a value. Parametrized by grid values. 
    - We can generalized to any function space. 

Neural implicits
- NN are function spaces
- parameterize a signal as a continuous function that maps the domain of the signal (i.e., a coordinate, such as a pixel coordinate for an image) to whatever is at that coordinate (for an image, an R,G,B color).
- Why?
    - We can represent complex geometry
    - Have adaptability in using parameters; extrapolates the data
    - Trivially differentiable
        - single shot reconstruction sitzmann et al 2019
        - Latent space interpolation park et al
        - Topology optimization zehnder et al 2021
- Why not?
    - imprecision: can also be difficult to quantify error so no guarantees
    - Downstream applications are hard because geometric data is stored in weights of neural networks
    - Possible to pick the wrong representation for the problem
- Working out the details
    - Sharp features: Fourier features tancik et al 2020 
    - Hybrid discrete continuous fields: to learn spatial features at grid points and we map the spatial points and features and output to scalar; instant NGP muller et al 2022
    - Sample points choosing: 
- Geometric operations
    - Change neural implicits to SDFs. It gives structure so geomtetric queries are easier.
    - How do we make sure neural implicit are SDFs? We can add regularization to loss function. 



