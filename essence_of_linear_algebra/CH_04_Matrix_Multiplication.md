---
layout: page
---

# CH 4 | Matrix multiplication as composition

#### Matrix "Multiplication"

* Matrix multiplication is the process of applying two transformations, one after the other

![Matrix Multiply](../resources/la_matrix_multiply.png)

* We also refer to matrix multiplication as **composition**

![Matrix Composition](../resources/la_matrix_composition.png)

#### Algebraic Process

* An abstract example looks like this:

|   |   |
|---|---|
|![Matrix X](../resources/la_matrix_multiply_process_1.png)|![Matrix Y](../resources/la_matrix_multiply_process_2.png)|

* A practical example looks like this:

|   |   |
|---|---|
|![Matrix X](../resources/la_matrix_multiply_process_3.png)|![Matrix Y](../resources/la_matrix_multiply_process_4.png)|

* In geometric terms:

    * Basis Matrix
![Basis Matrix](../resources/la_matrix_multiply_geometric_1.png)

    * Apply M1
![Apply M1](../resources/la_matrix_multiply_geometric_2.png)

    * Apply M2
![Apply M2](../resources/la_matrix_multiply_geometric_3.png)

    * The end product is the "product" or "composition" of M1 and M2

#### Caveat: Not Quite Multiplication

* Unlike normal multiplication, matrix multiplication is **not communative**

* **AB != BA**

* This is because the order of a matrix transformation matters
  * Applying **A** then **B** will produce a different output from applying **B** then **A**

