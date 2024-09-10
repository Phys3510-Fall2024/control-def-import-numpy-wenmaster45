[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/LMM68FzZ)
# README

We introduce control flow and some numpy basics in this week's activities.

## Notebooks

1. **Control Flow and Defining Functions Notebook** (`Control-flow-and-defining-functions.ipynb`)
    - This notebook introduces you to Python control flow structures such as `if`, `while`, and `for` loops.
    - You will also learn how to define your own functions using the `def` keyword and how to use these functions to solve problems.
    - **Recommended steps**:
        1. Read the explanation provided for each control flow structure.
        2. Work through the examples and make sure to run each cell.
        3. Complete the exercises at the end of each section to reinforce your understanding.

2. **Numpy Basics Notebook** (`numpy-basics.ipynb`)
    - This notebook covers fundamental operations in `numpy`, the core library for numerical computing in Python.
    - Topics include array creation, element-wise operations, matrix manipulations, and linear algebra operations.
    - **Recommended steps**:
        1. Begin by reviewing how `numpy` simplifies array manipulations compared to native Python lists.
        2. Follow the examples and run the code cells to observe how `numpy` handles matrices and vectors.
        3. Complete the exercises on element-wise operations, matrix multiplication, and linear algebra functions to solidify your knowledge.

## Additional Resources

If you need more help understanding the topics covered in these notebooks, feel free to explore the official Python and `numpy` documentation:
- [Python Documentation](https://docs.python.org/3/)
- [Numpy Documentation](https://numpy.org/doc/)

## Assginment

For this week's assignment, we are going to explore how different objects behave under different symmetry operations.

### Objective
By the end of this assignment, you should have a clear understanding of how different symmetry operations affect physical quantities such as scalars, vectors, and pseudoscalars, and an approach to implementing these operations using Python and numpy.

### Symmetry

Symmetry is a fundamental concept in physics. If a system obeys certain symmetries, the mathematical models that we use to describe it must also obey those symmetries. Everytime you have written down the equation for the energy of a system, or the force acting on a system, there has been an implicit appeal to your innate understanding of symmetry, or what has been developed in your experience in the world, or education in physics.


### The 'one-dimensional objects'

For this exercise, we are going to define 'one-dimensional objects' with vector operators, and use special symmetries to make sense of them. The four objects we are going to explore are:

1. scalar
2. pseudoscalar
3. polar vector
4. axial (pseudo) vector

We can construct thes objects out of Cartesian vectors (you may want these defined as numpy arrays to help with the assignment):

- a = [1, 0, 0]
- b = [0, 1, 0]
- c = [0, 0, 1]


### The symmetry operations

With these vectors defined, we can define the four objects, all aligned along the z-axis of a three-dimensional Cartesian space, by:

1. scalar: np.dot(a, b) # dot product
2. pseudoscalar: np.dot(c, np.cross(a, b)) # scalar triple product
3. polar vector: c # no operation
4. axial (pseudo) vector np.cross(a, b) # cross product

### 'Even' and 'odd'

We say that an object is *even* under a symmetry transformation if it does not change sign under the symmetry operation. The object is said to *odd* under a symmetry transformation if it changes sign. This is most easily seen by working with the polar vector `c = [0, 0, 1]`. We can imagine an arrow pointing up. If we, for example, perform a mirror operation for a mirror oriented in the xy-plane, the arrow would be pointing down. This is the same as if we multiplied `c` by `-1`. `c` is said to be *odd* under this mirror operation.

### An example of applying a symmetry operation

Take, for example the two following operations:

```python
identity = np.array(
         [[ 1, 0, 0]
         ,[ 0, 1, 0]
         ,[ 0, 0, 1]]
)
```

Applying this to the four objects is equivalent to:

id_scalar = np.dot(identity @ a, identity @ b)
id_pseudo_scalar = np.dot(identity @ c, np.cross(identity @ a, identity @ b))
id_polar_vec = identity @ c
id_axial_vec = np.cross(identity @ a, identity @ b)

Which, of course, has no effect. We have found the trivial relation that all of these objects are unchanged by the identity operation.

### The symmetry operations; assignment instructions

Define the following operations and find if the four objects are even or odd about these operations. Compile your results in a Jupyter Notebook called `symmetry.ipynb`. Include notes for yourself, explaining your apporach, and python cells showing your computational work. Include a table in MarkDown with your results at the end of the notebook (see below).

The operations are (I have defined the inversion operation for you):

```python
inversion = np.array(
               [[-1,  0,  0]
               ,[ 0, -1,  0]
               ,[ 0,  0, -1]]
)
```
- mirror_z: a mirror in the xy-plane
- mirror_y: a mirror in the yz-plane
- rotation_x_180: a 180 degree rotation about the x-axis


### How to create a table with markdown in Jupyter Notebook

To create a table in markdown, you can use `|` to separate columns, and `-` to create horizonatal lines. For example, I have started the table here:

| 1D object    | identity | inversion | mirror_z | mirror_y | rotation_x_180 |
|--------------|----------|-----------|----------|----------|----------------|
| scalar       | 1        |           |          |          |                |
| pseudoscalar | 1        |           |          |          |                |
| polar vector | 1        |           |          |          |                |
| axial vector | 1        |           |          |          |                |

Are any of these operators redundant?

If the system has these symmetries, The energy must be even under all of these symmetries. Assume that we have the following assignmnet:

Q_1 : scalar
Q_2 : pseudoscalar
Q_3 : polar vector
Q_3 = axial vector

Notice that the square of any of these terms, i.e. Q_i^2, is even under all of the symmetry operations. This is a generalization of the multiplication rules "even times even is even" and "odd times odd is even" for each symmetry. You can think about this as a sping-mass system where the energy stored in the spring is 1/2 k x^2. Each Q_i is the coordinate of a mass, and 1/2 k is whatever the coefficient of that is that gives us units of energy. Are any terms Q_i * Q_j possible? Why or why not? What about Q_i * Q_j * Q_k? These terms, if the exists, tell us how these "springs" can be coupled to each other.

### For those interested: Space-Time extension

This concept can be extended to space-time by adding an additonal operation `time-reversal` and treating every object as being a 4-vector where the first element is `c*t`. Then there are five new operators:

- identity + time-reversal
- inversion + time-reversal
- mirror_z + time-reversal
- mirror_y + time-reversal
- rotation_x_180 + time-reversal

and the objects become

- time-even scalar
- time-even pseudoscalar
- time-even polar-vector
- time-even axial vector
- time-odd scalar
- time-odd pseudoscalar
- time-odd polar-vector
- time-odd axial vector

Are there new Q_i * Q_j * Q_k terms allowed now? Are there patterns that you notice?

If you'd like to learn more about the application of this approach to condensed matter physics, have a look in this [recent paper by Jiri Hlinka](https://journals.aps.org/prl/abstract/10.1103/PhysRevLett.113.165502)
