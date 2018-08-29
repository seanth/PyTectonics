# ABOUT
PyTectonics is a 3d plate tectonics simulator written in Python to provide realistic terrain generation for enthusiast world builders.

PyTectonics is a principled model. It aims to use simple yet scientifically defensible models that may be easily understood by nonexperts and modified by developers. A 3D framework is used to provide a solid foundation for modeling that is grounded in reality. Python is used to allow access from a wider audience of developers.

The model is open source and licensed under version 2.0 of the Creative Commons Non Commercial Attribution License.

### Community
Before going any further, consult our growing documentation to see if you can address the issue, yourself. 
            Documentation is wiki based, and if you can't find what you need you can always add on to it for posterity</p>
            <a href="http://sourceforge.net/p/pytectonics/wiki/Home/">Project Wiki</a>
            <p>Our project forums target specific questions...</p>
            <a href="http://sourceforge.net/p/pytectonics/discussion/">Project Forums</a>
            <p>...and issues with the model itself can be posted on our bug tracker</p>
            <a href="http://sourceforge.net/p/pytectonics/tickets/">Project BugTracker</a>
### The Developer
If all else fails, drop me a line and I'll try to get back to you as soon as I can.</p>
            <a href="mailto:davidson1@web.sourceforge.net">davidson1@web.sourceforge.net</a>
### Acknowledgements
* <a href="http://vpython.org/index.html">Vpython</a>
* <a href="http://www.scipy.org">Scipy</a>
* <a href="http://www.numpy.org">Numpy</a>
* <a href="http://www.python.org/">Python</a>
* <a href="http://creativecommons.org/">Creative Commons</a>
* <a href="https://sourceforge.net/">Sourceforge</a>
### Predecessors
* <a href="http://markjstock.org/pages/builder.html">Plates</a>: Originally a direct descendant, pyTectonics began as a python port for the Plates model. It has since been rewritten to the point the two share little in common.
* <a href="http://sourceforge.net/projects/platec">PlaTec</a>: In a case of convergent evolution, pyTeconics has come to adopt several methods similar to those in PlaTec. Plates, for instance, are respresented in both models as grids on which cells are mapped to represent crust. Nevertheless, PlaTec remains a 2D model with all the costs and benefits that imparts.
* <a href="en.wikipedia.org/wiki/SimEarth">SimEarth</a>: The spiritual precedent for PyTectonics







# NEWS
New Release: 0.3a
A new release comes to pytectonics:

   cleaner
   faster
   speed control
   thickness map
   docking
   dropped scipy dependency
   I'd originally intended 0.3 to add the supercontinent cycle, but with how the work so far shapes up it seems like a new release is in order, anyways.

Perhaps most important this release is the docking functionality. Previous versions differed in how collision was performed between landmass. In real life, colliding continents have the potential to interrupt the plates they move on. Smaller, more common landmasses such as those found in island arcs however dock to larger landmasses without interrupting plates. Pytectonics previously handled the former without the latter. What made matters worse was how velocity was affected by collision - the model took a naive approach, stopping plates entirely when collision was detected. Effectively, this caused plates in the long run to stop moving, oftentimes for no reason other than hitting some insignificant island. The most recent version handles docking, though, appending crust from smaller colliding landmass to the plate of the larger landmass. Velocity is also now altered by collision in a much more sensible manner that assumes the conservation of angular momentum. This felt to me a good first order approximation given I wanted the model to remain simple without considering things like mantle convection. It still seems to me a bit naive given the timescales involved, but a brief look through literature really does seem to suggest that angular momentum is conserved.

On a bit of a side note, SciPy should now no longer be needed for subsequent versions. Previous versions used SciPy largely for the kd-tree library, allowing efficient lookups of nearest neighbors through 3d cartesian coordinates. Over the course of many commits though I've found it much faster to drop the 3rd dimension and determine neighbors based upon 2d spherical coordinates, which is rather incompatible with SciPy's kd-tree implementation. As of the previous version, kd-trees were only used upon initialization to determine the nearest plates and continents to each grid cell. Beyond that, SciPy did provide some functionality through the use of obscure mathematical constants such as the golden ratio, but that hardly warrants the dependency from the user's perspective.
