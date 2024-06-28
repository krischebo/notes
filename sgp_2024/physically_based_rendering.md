# Physically-based rendering (6/23, 11AM)

## PART 1: Introduction

People care about visible light and how they interact with different objects. First they cared about heat (PDEs) and then cared about light due to the rise of computer graphics.

We want to know the steady state color of a  point is and the rendering equation (a general equation that consolidates all graphically states) models that.

Understanding the rendering equation’s intuition:
- Dominant light source is considered first 
- Then emitters of light reflect on other surfaces. So any given point is impacted by the reflections of light from other objects. Though, it may dominated by the light source, there are less obvious impacts from other objects.
- Position of eye also matters when looking at a point. 

READ ⬇️
The rendering equation form
- The rendering equation has a recursive element about light sources and its reflections.

BRDF: Bidirectional reflection distance function
- Ratio between radiance and irradiance; terms from radiometry
- Radiance is the radiant flux emitted, reflected, transmitted, or received by a given surface, per unit solid angle per unity projected area.
- Spherical coordinates: measure of height angle is altitude and its horizontal counterpart is azimuth.

BSDF is the greater function = BRDF + BTDF + BSSRDF. Light through different surfaces, materials, sources, and what not. The utimate light equation.


## PART 2: Geometric simplification

Cloth 
- geometry
    - Woven cloth
        - Underlying structure is super complicated
        - However, single fibers are relatively simple and 10-100 micrometers 
    - We have to capture these micrometer properties to get a realistic render
    - Different clothes and materials and weaving style impacts how we render those cloths
- Rendering
    - No. of cloth fibers are too high
    - Super memory intensive
    - Violation of energy conservation
    - Complex fiber arrangement
    - Complex multiple scattering
    - Not all fibers are perfect; fly-away fibers

This part about different models that render cloth in a time and memory efficient manner. The tradeoff is speed or fidelity <- like most things.

Solving these problems
- Reduce the no. of fiber & Aggregate the appearance <- will be realistic
- Fewer fibers with original fiber <- drier, harder, and brighter
- Aggregation is important.

