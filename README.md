# Brugia_metabolic_network
Files pertaining to our paper on the genome-scale metabolic network reconstruction for Brugia malayi
- Curran, Grote et al., 2020. "Modeling the metabolic interplay between a parasitic worm and its bacterial endosymbiont allows the identification of novel drug targets", _eLife_ https://doi.org/10.7554/eLife.51850

Model files
===========
This repository contains one model (model_bm_6) in two formats (Excel and SBML). It also contains 10 variants of that model, for which the reaction bounds are constrained by gene expression data from 10 different B. malayi life stages. To calculate these constraints, the reaction bounds for each life stage are scaled relative to the maximal FPKM value for that reaction accross all life stages. The exception is if one life stage had no measured expression of some gene, the cognate reaction was left unconstrained.
The models contain three compartments: the cytosol, the mitochondria, the Wolbachia cell. Transporters exist between the cytosol and the environment, the cytosol and the mitochondria, and the cytosol and Wolbachia.

Life stages
===========
The 10 life stage-specific models are:
L3
L3D6 (6 days post infection; during L3-L4 molting)
L3D9 (9 days post infection; during L3-L4 molting)
L4
F30 (adult female, 30 days post infection)
F42 (adult female, 42 days post infection)
F120 (adult female, 120 days post infection)
M30 (adult male, 30 days post infection)
M42 (adult male, 42 days post infection)
M120 (adult male, 120 days post infection)

Specific conditions
===================
All models are set up in high oxygen high glucose (HOHG from our publication) conditions. To achieve the conditions in our publication, modify the upper bounds of the reactions 'DIFFUSION_2' and 'CARBON_SOURCE' to:
High oxygen & high glucose (HOHG) = 580, 250
High oxygen & low glucose (HOLG) = 580, 45
Low oxygen & high glucose (LOHG) = 90, 250
Low oxygen & low glucose (LOLG) = 90, 45

Most filarial nematodes, including B. malayi, contain an endosymbionic bacteria from the genus Wolbachia. These bacterial cells provide some metabolic reactions, but also consume nutrients to survive. Our model deals with this with the concept of a Wolbachia weight value, which indicates the relative amount of Wolbachia available relative to B. malayi. This scales the maximum capacity of the reactions in the Wolbachia compartment, but also scales the Wolbachia portion of the biomass objective function. So the higher the weight, the more flux that can be processed by Wolbachia reactions, and the more nutrients required by Wolbachia. All models have a weight of 0.1, meaning the Wolbachia reaction bounds are (-100, 100) while cytosolic and mitochondrial reaction bounds are (-1000, 1000), and the overall objective function requires 0.1 units of Wolbachia biomass for every 1 unit of Brugia biomass.
