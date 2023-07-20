---
title: "REGISTRATION MODULE"
excerpt: "Implements a registration class that can accomodate calls to other methods in a unified manner."
collection: software
toc: true
---
{% include base_path %}



The main classes within this module are
- ShapesRegistration - to perform registration with different methods
- RegMetrics - to evaluate results from registration under different metrics.

Below you can find details on these two modules, as well as a third section about the current registration methods implemented.


## ShapesRegistration

 This is a generic class that can then be used to create specific classes for a desired registration algorithm by implementing the method <i>pair_registration</i>.
We will first provide an overview of the class and then detail how <i>pair_registration</i> must be correctly implemented for new methods.
Currently, the implemented algorithms are ICP, BCPD and GPSF.


### simple_registration
 The way to perform registration is with a call to the method <i>simple_registration</i>, which receives as input a <i>template</i> (numpy array),
a <i>dataset</i> (ShapeDataset object) and an <i>id_list</i> (list of integers) of the shapes to register. The registration can be performed in parallel by setting the flag <i>flag_parallel</i> to true.
The output is an object of class RegDataset. Below is a simplified example with the ICP class.



```python
obj_reg = IcpRegistration()
reg_dataset = obj_reg.simple_registration(template, dataset, id_list, flag_parallel)    
```



### Create a registration method class 

 Any registration class inherits from ShapesRegistration. In order to completely define a new method, it is necessary to define its attributes (specific parameters to the algorithm in question)
                        and to implement the method <i>pair_registration</i>.


<i> pair_registration</i>  receives as input two numpy matrices, the target and the source, where the source is to be deformed to fit the target.
                        The specific steps of the method are then implemented. It must return a numpy matrix of the same dimensions as the source (with the obtained deformations) and
                        a correspondence vector with the ids of the target corresponding to each template point - if no correspondence is found that element is set to nan.
                        Below you can find examples for the implemented methods <a href="#ICP">ICP</a>, <a href="#BCPD">BCPD</a> and <a href="#GPReg">GPReg</a>.


## RegMetrics

This class requires as input one object ShapeDataset with the original dataset and one object RegDataset with the output of a registration procedure.
                        It computes a given number of pertinent metrics and displays the results. Below we describe the most useful methods.


- plot_dist_metrics_by_shape - produces 3 bar plots with 3 different distance measures: average distance between the deformed template and target, average difference between the original template and target and average difference in the target for correspondences found.
![Plotting result](../../images/reg_metrics_pic_distances.png)

- plot_corr_metrics_by_shape -  plots correspondences metrics by shape
- plot_outlier_metric_by_shape -   plots outliers metrics by shape (accuracy, recall and precision)
- plot_missing_metric_by_shape -  plots missing data metrics by shape (accuracy, recall and precision)


## Implemented Methods
We provide the classes for a few state-of-the-art methods.
Note that the code for some of the methods must be obtained by the authors original repositories (links are provided at convenient locations).
It serves as a template, so that users can easily implement any method of their choice.
When available, we prefer the python implementation, but it often happens that it is not provided. We resort to the matlab engine for python in order
to execute the matlab code (i.e. some time will be wasted to perform this step, so it may not be the most suitable option depending on the settings of your project).

### Iterative Closest Point (ICP)

This methods is implemented with the open access library <a href="http://www.open3d.org/docs/release/index.html">Open3D</a>, for both
<a href="http://www.open3d.org/docs/release/tutorial/pipelines/icp_registration.html">Point-to-Pont ICP</a>  and
<a href="http://www.open3d.org/docs/release/tutorial/pipelines/icp_registration.html">Point-to-Plane ICP</a>. The necessary outputs are obtained resorting to attributes
<a href="http://www.open3d.org/docs/latest/python_api/open3d.pipelines.registration.RegistrationResult.html?highlight=correspondence_set#open3d.pipelines.registration.RegistrationResult.correspondence_set
">correspondence_set</a> (appropriately converted to template view) and <a href="http://www.open3d.org/docs/latest/python_api/open3d.pipelines.registration.RegistrationResult.html?highlight=transformation#open3d.pipelines.registration.RegistrationResult.transformation
">transformation</a>. Points with larger distance than <i>max_dist</i> are set to <i>nan</i> in the output.

#### Point-to-Point

This variant takes as input <i>max_dist</i> (maximum distance allowed for corresponding points), <i>scaling</i> (if True scaling will be estimated) and <i>initial_transf</i> (initial transformation applied to template - if not defined is set to identity matrix).
Below we present an example of usage.

```python
max_dist = 0.25
icp_reg = IcpRegistration(reg_type = 'point_to_point', max_dist=max_dist, scaling=False)
flag_parallel = False
id_list = 'all'
reg_dataset = icp_reg.simple_registration(template, dataset, id_list, flag_parallel)    
```

#### Point-to-Plane
 
In terms of implementation, the difference to the previous method is that normals are computed with
a call to <a href="http://www.open3d.org/docs/latest/python_api/open3d.geometry.PointCloud.html?highlight=estimate_normals#open3d.geometry.PointCloud.estimate_normals">estimate_normals()</a>
and the scaling parameter is not applicable. Therefore, this variant can be coded as
```python
icp_reg = IcpRegistration(reg_type = 'point_to_plane', max_dist=max_dist)
```

### Bayesian Coherent Point Drift (BCPD)

BCPD is implemented with the authors <a href="https://github.com/ohirose/bcpd#point-set-registration">original code</a>, where the reader may also find an extensive description of its parameters and general usage, as
well as the related paper. Our code is merely an encapsulation of their function within our python framework and so we present an example of code with the parameters in our function corresponding to the BCPD
original parameters - for further details refer to the mentioned page. We have included the most relevant parameters, but it is trivial to include additional ones, if necessary.

For the encapsulation, <a href="https://it.mathworks.com/help/matlab/matlab-engine-for-python.html">MATLAB Engine</a> is used for a call to matlab in order to execute the necessary commands.
This calls for the script <i>\Other_methods\BCPD\bcpd_register.m</i> which does the necessary transformations between the bcpd setting and ours (and vice-versa).
The temporary files required for BCPD are stored under <i>'resources\temp_files'</i>. Note that sometimes the registration with BCPD leads to failure and does not produce any output files -
in this case, the output of <i>pair_registration</i> will be None for both variables.

```python
    omega = 0.1 #  -w Omega: outlier probability
    lmbd = 0.1 #  -l  Lambda: expected length of deformation vectors.
    beta = 2 #  -b  beta: range where deformation vectors are smoothed.
    gamma = 3 #  g  gamma: randomness of the point matching at the beginning of the optimization

    # convergence
    cov_tol = 1e-4 # -c Convergence tolerance.
    max_VB_lopps = 30 # -n maximum number of VB loops
    min_VB_loops = 500 # -N minimum number of VB loops

    normalization = 'e' # -u normalization

    flag_std_acc = 0 # if set to 1 accelerates with default parameters

    bcpd_reg = BcpdRegistration(omega= omega, lmbd = lmbd, beta = beta, gamma = gamma,cov_tol = cov_tol, max_VB_lopps = max_VB_lopps, min_VB_loops = min_VB_loops, flag_std_acc=flag_std_acc)
```

### Gaussian Process Registration 
To be added soon (upon acceptance of the related manuscript).



