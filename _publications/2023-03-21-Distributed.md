---
title: "Distributed Solution of the Inverse Rig Problem in Blendshape Facial Animation"
collection: publications
permalink: /publication/2023-03-21-Distributed
excerpt: ''
date: 2023-03-21
paperurl: ''
citation: 'S. Racković, C. Soares, D. Jakovetić, “Distributed Solution of the Inverse Rig Problem in Blendshape Facial Animation,”
	SIGGRAPH Asia 2023, Technical Communications, 24, 1-4, (2023).'
paperoglink: 'https://dl.acm.org/doi/abs/10.1145/3610543.3626166'
githublink: 'https://github.com/stevorackovic/FacialAnimation/tree/master/Scripts/DistributedSolution/ADMM'
---

Abstract 
--------

The problem of rig inversion is central in facial animation as it allows for a realistic and appealing performance of avatars. With the increasing complexity of modern blendshape models, execution times increase beyond practically feasible solutions. A possible approach towards a faster solution is clustering, which exploits the spacial nature of the face, leading to a distributed method. In this paper, we go a step further, involving cluster coupling to get more confident estimates of the overlapping components. Our algorithm applies the Alternating Direction Method of Multipliers, sharing the overlapping weights between the subproblems. The results obtained with this technique show a clear advantage over the naive clustered approach, as measured in different metrics of success and visual inspection. The method applies to an arbitrary clustering of the face. We also introduce a novel method for choosing the number of clusters in a data-free manner. The method tends to find a clustering such that the resulting clustering graph is sparse but without losing essential information. Finally, we give a new variant of a data-free clustering algorithm that produces good scores with respect to the mentioned strategy for choosing the optimal clustering.

This paper was selected for the [Association for Computing Machinery (ACM) Showcase on Kudos](https://www.growkudos.com/publications/10.1145%25252F3610543.3626166/reader)!



