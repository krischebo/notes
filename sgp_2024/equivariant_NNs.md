# Equivariant NNs	(6/22,9AM)

## PART 1: ROBIN WALTERS

Equivarance: In mathematics, equivariance is a form of symmetry for functions from one space with symmetry to another. A function is said to be an equivariant map when its domain and codomain are acted on by the same symmetry group, and when the function commutes with the action of the groupIn mathematics, equivariance is a form of symmetry for functions from one space with symmetry to another. A function is said to be an equivariant map when its domain and codomain are acted on by the same symmetry group, and when the function commutes with the action of the group.

Incorporating symmetry into neural networks:
- Identify system symmetries
- Build network constrained by symmetric
- Optimize

Formalizing symmetry
- Abstract symmetry template: C_4 = {1,r,r2,r3|r4=1}; cyclic group
- Can represent as 2x2 matrices or 4x4 when cyclic group demands

Equivariant functions
- F is G-equivariant if f(p_in(g)x = p_out(g)f(x)
- When two functions change the same way: equivariant

How to design neural network architecture with symmetry in them? <- MAIN QUESTION

MAIN IDEA: equivariant linear layers and equivariant activations => equivariant networks; equivariance is preserved through function composition

What Is equivariant layer and activation?
- Constraining neural networks with equivariance reduces the no. of parameters that are needed. For example, if the two layers are certain properties— rotation or cyclic— you want them to be kinda interchangeable. So the matrix that transforms them has to have some symmetry, which reduces the no. of variables because the matrix must have structure.
- We need activation functions that do not zero stuff that has to be rotated and what not. 
- So our entire model shrinks to a smaller search space of only equivariant functions. Huge dimensional reduction. 

Applications of equivariant NN
- Physical dynamics: because natural stuff has geometry embedded in them
- Turbulent flow prediction: essentially a vector fields of forward moving functions. Goal: to predict future of these movements or flow of fluids (still future)  Navier Stokes eqn. Is invariant to scaling. So scaling is symmetric and can be used. 
- Pose prediction: to teach networks to learn low-dimensional stuff from a lower-dimension. Ex: learn about 3D stuff from just images. Task: to understand rotation or position in 3D space from an image.  Standard regression methods struggle in the open-world setting where a single true oration may not exist. Result: hybrid equivariance model; CNN in the beginning and then orthogonal projection to become 3D (SO(3)).
How do build scaling equivariance?
- We translate and scale a kernel across all the input. So the beginning function changes over everything. Think of kernel in groups.

## PART 2: JUNG PARK
Unknown group actions
- 3D rotation is not as simple as 2D rotation since pixels might not evenly move and some pixels might not even be visible.
- Symmetric Embedding Network (SEN) Key idea: pair SEN with downstream equivariant networks and train end-to-end. 
- SEN Meta-Architecture: can adapt to different domains

Assumptions of equivariant model
- Equivariant task function
- Invariant input distribution: x~D, pD(x) = pD(gx)

Diff kinds of equivariance:
- Incorrect: points do not end up where they were originally
- Extrinsic: we see new data points that are a transformation of the original 
- Correct: opposite of incorrect

Can extrinsic models be useful?
- Conventional wisdom: harmful since it is an incorrect inductive bias
- But enforcing generalization to our of distribution points could make the decision boundary easier to find; because we have new points to draw a line around

QUESTION: 
- can we measure degree of extrinsic equivariance?
    - Not really
