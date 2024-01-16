---
layout: project
title: Simulating Hydraulic Erosion
description: Using fluid dynamics to create believable terrains.
img: ../img/FluidDynamics/FluidDynamicsThumbnail.jpg
published: true
---

This is my final year dissertation project to create realistic terrains through simulating hydraulic erosion applied to fluid dynamics on procedural heightmaps.

<div class="img_row">
	<img class="col four" src="{{ site.baseurl }}/img/FluidDynamics/1_simulationRunning.jpg" alt="" title="example image"/>
	<img class="col four" src="{{ site.baseurl }}/img/FluidDynamics/2_simulationFinished.jpg" alt="" title="example image"/>
	<img class="col four" src="{{ site.baseurl }}/img/FluidDynamics/3_settings.jpg" alt="" title="example image"/>
	<img class="col four" src="{{ site.baseurl }}/img/FluidDynamics/4_finishedMesh.jpg" alt="" title="example image"/>
</div>
<div class="col three caption">	
	From top-left to bottom-right: in-process simulation, finished simulation, custom settings, the finished terrain mesh in Unity.
</div>

Smoothed Particle Hydrodynamics (SPH) is the implemented fluid dynamics method in which the hydraulic erosion simulation is applied. SPH is a simulation method whereby the fluid is represented by particles that interact with each other and are smoothed using a kernel function. Within the simulation loop, each particle builds a neighbour searcher and list and calculates density, pressure from neighbouring particles, viscosity force, and external force of gravity to apply to it's velocity and calculate it's new position. collisions are resolved and the loop continues for the input number of frames. A hashing algorithm is used to accelerate the neighbour search by mapping particles into a grid of buckets based on position, determined by a spatial hashing function. The kernel function spreads out particle values over the kernel radius and interpolation is used to measure physical quantities at a given point by looking up nearby particles and calculating a weighted average.

The fluid particles simulate sediment collection and deposition through reducing and increasing the height of collided points on the heightmap relative to their velocity, change in elevation, particle density, and pressure. This allows for erosion to occur across the terrain relative to the flow of fluid in order to achieve results appropriate to the goal of creating realistic terrains. More erosion occurs in areas of high density relative to those of low density and particles are 'reset' and placed randomly above the terrain after flowing over the edge to simulate rainfall and create small streams within the mesh due to the velocity gain while falling.