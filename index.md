# Derek Everett
<derekeverett@gmail.com>

# Table of Contents
1. [Studying Heavy-Ion Collisions](#studying_hic)
2. [Computational Modeling of Physical Systems](#comp_model)
3. [Statistical Model Emulation](#stat_emu)
3. [Statistical Inference](#stat_infer)

### Studying Heavy-Ion Collisions<a name="studying_hic"></a>
The collisions of heavy nuclei at very high energies performed at the [Relativistic Heavy Ion Collider](https://www.bnl.gov/rhic/) and [Large Hadron Collider](https://home.cern/science/experiments/alice)) can produce an exotic state of matter called [Quark-Gluon Plasma](https://en.wikipedia.org/wiki/Quark%E2%80%93gluon_plasma). 
This phase of matter existed in the infant universe about one microsecond after the [Big Bang](https://en.wikipedia.org/wiki/Big_Bang). 

To understand the properties of this phase of matter, we develop physical models and compare their predictions to the data measured in the labaratory. Disentangling the properties of the collision at early times given only the finally measured particles requires us a methodology for inference. We use [Bayesian inference](https://en.wikipedia.org/wiki/Bayesian_inference) as a systematic way to make conclusions given the observed data. 

I have been a contributing member of the [JETSCAPE collaboration](jetscape.org), designed to tackle both physical and statistical modeling. A review of some of the work by our particular team can be found [here](http://jetscape.org/sims/). 


### Computational Modeling of Physical Systems<a name="comp_model"></a> 

The models for Heavy Ion Collisions often involve many different stages, described by differing underlying physics. 

The initial conditions describing the deposited matter after the collision can be propagated through many differing physical models. A very simple model assumes that the particles expand isotropically in the plane transverse to the beam direction. 
I've developed a [freestreaming model](https://github.com/derekeverett/freestream-milne) to solve the expansion in two or three spatial dimensions. More complicated models assume that the particles can interact. I've also developed [KTIso](https://github.com/derekeverett/KTIso) to simulate the expansion of interacting particles. It determinanistically solves the [Boltzmann equation](https://github.com/derekeverett/KTIso).  

A core component of many models which are able to describe data well is viscous hydrodynamics. I've assisted in the continued development and maintenance of a [relativistic viscous hydrodynamic code](https://github.com/derekeverett/cpu-vh), additionally with a [version optimized for Graphics Processors](https://github.com/derekeverett/gpu-vh). 

After a phase of hydrodynamic expansion, the fluid cools and breaks apart into hadrons, which finally reach the detector. I've assisted in the development of a [model](https://github.com/derekeverett/iS3D) which simulates this [particlization process](https://arxiv.org/abs/1912.08271). 

Finally, observables are calculated which can be compared with experimental data. The observables predicted by a particular model at the point in parameter space which maximizes the likelihood is shown below. 


<div style="text-align:center">
<img src="figs/observables_fit_MAP.png" alt="Heavy Ion Observables" width="500"/>
</div>

*Predictions of the model with Grad particlization at the point in parameter space of maximum likelihood.*


### Statistical Model Emulation<a name="stat_emu"></a>

The computational physics model we use to generate observables given the physical parameters includes two or three-dimensional hydrodynamic solvers as well as Monte Carlo Boltzmann Solvers. Given a single set of parameters, evaluation of the model can exceed fifty-thousand core-hours. This makes exploring the likelihood function (comparing the model-data misfit) intractable with the computational model.

Instead, we train a statistical surrogate or *emulator* as a proxy for our model when we perform likelihood evaluation in Bayesian inference. The emulation introduces an additional source of uncertainty.
In practice, we perform a dimensionality reduction of the observables via [principal component analysis](https://en.wikipedia.org/wiki/Principal_component_analysis). Then, each principal component is modeled by a Gaussian process.

I've written a introduction to Bayesian inference with a Gaussian process model emulator and Markov Chain Monte Carlo [here](https://github.com/derekeverett/simple_bayes_with_GP/blob/master/Infer_Shear_Viscosity_from_Flow_GPy.ipynb).  

 

### Statistical Inference<a name="stat_infer"></a>

Given the experimental observables, we want to infer what were the properties and dynamics of the system. This is a problem well-suited for Bayesian inference. 

We can estimate the specific shear and bulk-viscosities of the Quark Gluon Plasma fluid by performing [Bayesian parameter estimation].
The entire model can contain up to seventeen uncertain parameters that we want to infer. Among them are the parameters controlling the transport properties, the specific shear and bulk viscosities. 


<div style="text-align:center">
<img src="figs/viscous_posterior_overlay.png" alt="Heavy Ion Observables" width="500"/>
</div> 

*The estimated specific bulk (left) and shear (right) viscosities of the Quark Gluon Plasma, as a function of temperature. The 90% credible intervals are shown for three different models in blue, red and green.*

Making robust estimates of the transport properties requires us to include the model uncertainties which enter various other stages of the collision. For instance, we must simultaneously estimate properties of the initial conditions, because they are correlated by the model with the transport properties. All together, we vary seventeen model parameters. The one-dimensional and two-dimensional posteriors for select parameters are displayed in the corner plot below. 

<div style="text-align:center">
<img src="figs/posterior_ic_fs_tsw.png" alt="Heavy Ion Observables" width="700"/>
</div>

*The posterior of select model parameters, for two different models in blue and red.*

Besides the uncertainties which exist in the physical parameters describing the system, there can be additional sources of model uncertainty in the dynamical models that we employ. Such discrete sources of model uncertainty pose the problem of model selection. We investigate this question by calculating the [Bayes factor](https://en.wikipedia.org/wiki/Bayes_factor) -- the odds that the experimental data were produced by a certain model relative to another model. The Bayes factor can depend sensitively on the priors chosen for each model -- if certain priors were relaxed or constrained, our selection of which model the data prefer can change! To address this sensitivity, the [Bayes factor surface] was proposed.
Bayes factor surfaces for three different models are shown below.

<div style="text-align:center">
<img src="figs/log_odds_grad_ce.png" alt="Bayes factor surface" width="400"/>
</div>

*The predicted log-odds (color contours) between two different models, as a function of two prior hyperparameters.*  

