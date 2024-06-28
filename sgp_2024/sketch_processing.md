# Sketch processing (6/22, 2PM)

## FUNDAMENTALS
Sketches are not photos. They are stylized and heavily distorted. Processing has to be guided by perception/data, not simple metrics.

Raster vs vector
- Raster: made of pixels
- Vector: made of curves and precise lines

What is inside a sketch?
- Strokes, endpoints, and junctions
- Junctions can be real or intended that depends on perception
- Occluding contours
    - Points where surface normal is perpendicular to the view direction
- Ridges and valleys
    - People identify these and draw them. We can somewhat process these.

Can we just use synthetic sketches? No.
- 60% of drawn content is consistent with computer-generated output. Wang et al. 2021
- Sketches have different stroke types, drawn for different purposes. Those connect at junctions and intersections. 

Shapes sketches represent
- 2D shape
    - stroke only: non-manifold
    - With fills and thickness: 2-manifold
    - Clusters: can indicate either approximate curve or variable width
    - Implied junctions or continuations in sketches is ambiguous too
    - Hours or not? Inside vs outside
    - LOT OF AMBIGUITY
- 3D
    - Smooth unless shown otherwise, but might indicate implication by artist
SUMMARY of problems: cannot interpret artist intention in strokes
Core challenges
- Topology
    - Problems
        - Which stroke is connected to which? 
        - Is the shape closed?
        - Is a particular stroke a mistake or a feature? We might not know how to vectorize it
        - Research: do strokes form clusters? Is there a way to quantify this ambiguity to become less ambiguous?
        - Fine details vs. overdrawing
        - How to segment or break into clusters?
    - Solutions
        - Learning
        - Reeb graph: study topology of shape by studying how functions work on the shape. example: look at height function changes on a donut. You draw isolines and try to contract it onto a single point. At saddle points, you have two isolines, so cannot contract to a single point. 
            - Used in vectorization algorithms.
            - Stroke cluster -> reef graph
            - Function = cluster paramterization
- Background vs foreground
    - Problems
        - Is shadow foreground or background?
            - Deep learning is the only way
        - What about vectors?
    - Solution
        - Cech complex: draw an epsilon-ball around every point. Then create a simplex wherever ball intersect. Myronova et al. 2023
- Junctions
    - Problems
        - where are endpoints, junctions, and intersections
        - Hidden contours: we draw manually. Should we connect endpoints heuristically with splines?
        - Occlusions
    - Solution
        - CNN that give heat maps of where endpoints are.
- Tangents
    - Problems
        - Tangents are near end points and junctions or of overdrawn strokes.
        - Where to connect on the stroke?
    - Solution
        - Directional and frame fields: discretizes the choices. May fail when there are multiple tangents
- Parameterization
    - Problem
        - To figure out its arc length parameterization of a cluster
        - Undertanding which point is adjacent to which
    - Solution
        - Eikonal equations are solutions
- Centerlines
    - Problem
        - Finding centerlines of a bitmap line drawing. In the stroke, what is the middle?
    - Solution
        - Gradient descent, Noris et al. 2012
        - Unsigned distance field, Yan et al. 2024
- Stroke vs. fill
    - Problem
        - Self-explanatory. Open problem
- Correspondences
    - Problem
        - A correspondence between strokes suggests point wise correspondence. Creating a 1-1 map?
        - But it can be 1-many or 1-none which can be difficult. Matching sketches with different poses face this problem
    - Solution
        - No good solution, but some make-shift:
        - Joint tracing
        - Optical flow
            - You think of the movement. A vector field deforms into another drawing
        - Functional maps
            - Color can represent correspondence but may not be good in practice. 

IMPLICATIONS: having principled solutions to any challenge can be a big deal for applications

## APPLICATIONS
- Sample to sequence algorithms using time series 
- Lot of open problems
