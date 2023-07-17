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

## Implemented Methods



![Plotting result](../../images/example_reg.png)
