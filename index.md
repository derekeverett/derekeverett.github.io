# Derek Everett
<derekeverett@gmail.com>

## Studying Heavy-Ion Collisions
The collisions of heavy nuclei at very high energies performed at the [Relativistic Heavy Ion Collider](https://www.bnl.gov/rhic/) and [Large Hadron Collider](https://home.cern/science/experiments/alice)) can produce an exotic state of matter called [Quark-Gluon Plasma](https://en.wikipedia.org/wiki/Quark%E2%80%93gluon_plasma). 
This phase of matter existed in the infant universe about one microsecond after the [Big Bang](https://en.wikipedia.org/wiki/Big_Bang). 

To understand the properties of this phase of matter, we develop physical models and compare their predictions to the data measured in the labaratory. Disentangling the properties of the collision at early times given only the finally measured particles requires us a methodology for inference. We use [Bayesian inference](https://en.wikipedia.org/wiki/Bayesian_inference) as a systematic way to make conclusions given the observed data. 

I have been a contributing member of the [JETSCAPE collaboration](jetscape.org), designed to tackle both physical and statistical modeling. A review of some of the work by our particular team can be found [here](http://jetscape.org/sims/). 


### Computational Modeling of Physical Systems 

The models for Heavy Ion Collisions often involve many different stages, described by differing underlying physics. 

The initial conditions describing the deposited matter after the collision can be propagated through many differing physical models. A very simple model assumes that the particles expand isotropically in the plane transverse to the beam direction. 
[`freestream-milne`](https://github.com/derekeverett/freestream-milne) is a code I've designed to to model this expansion in two or three spatial dimensions. More complicated models assume that the particles can interact. I've also developed [KTIso](https://github.com/derekeverett/KTIso) to simulate the expansion of interacting particles. It determinanistically solves the [Boltzmann equation](https://github.com/derekeverett/KTIso).  

A core component of many models which are able to describe data well is viscous hydrodynamics. I've assisted in the continued development and maintenance of a [relativistic viscous hydrodynamic code](https://github.com/derekeverett/cpu-vh), additionally with a [version optimized for Graphics Processors](https://github.com/derekeverett/gpu-vh). 

After a phase of hydrodynamic expansion, the fluid cools and breaks apart into hadrons, which finally reach the detector. I've assisted in the development of a [model](https://github.com/derekeverett/iS3D) which simulates this [particlization process](https://arxiv.org/abs/1912.08271). 

Finally, observables are calculated which can be compared with experimental data. 

### Statistical Inference 

Given the experimental observables, we want to infer what were the properties and dynamics of the system. This is a problem well-suited for Bayesian inference. 

We can estimate the specific shear and bulk-viscosities of the Quark Gluon Plasma fluid by performing [Bayesian parameter estimation].
The entire model can contain up to seventeen uncertain parameters that we want to infer. Among them are the parameters controlling the transport properties, the specific shear and bulk viscosities. 

![Specific Shear and Bulk Viscosities](figs/viscous_posterior_overlay.png) 
*The estimated specific bulk (left) and shear (right) viscosities of the Quark Gluon Plasma, as a function of temperature $T$. $90\%$ credible intervals are shown for three different models in blue, red and green.*

Making robust estimates of the transport properties requires us to include the model uncertainties which enter various other stages of the collision. For instance, we must simultaneously estimate properties of the initial conditions, because they are correlated by the model with the transport properties. All together, we vary seventeen model parameters. The one-dimensional and two-dimensional posteriors are displayed in the corner plot below. 

![Specific Shear and Bulk Viscosities](figs/posterior_full.png) 
*The posterior of all model parameters for two different models in blue and red.*

