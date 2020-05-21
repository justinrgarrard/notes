---
layout: page
---

# CH 7 | Inverse matrices, column space and null space

#### Using Matrixes for Great Good

* One of the primary uses of matrixes is solving linear systems of equations (usually through computer programs)

![System of Equations](../resources/la_system_of_equations.png)

* This often requires the ability to "undo" a matrix by using the **Inverse Matrix**

![Inverse System](../resources/la_inverse_system.png)

![Inverse System 2](../resources/la_inverse_system_2.png)

#### The Inverse Matrix

* So long as the determinant of a matrix is not zero, there is exactly one inverse matrix

|   |   |
|---|---|
|![Pre Inverse](../resources/la_inverse_pre.png)|![Post Inverse](../resources/la_inverse_post.png)|

* There is no inverse matrix when the determinant of a matrix is zero, as you cannot "unsquish" space

![Unsquish](../resources/la_zero_determinant.png)


#### Rank and Column Space

* Matrixes can be defined by their **rank**, which represents the number of dimensions the space was compressed into. This is especially helpful for zero determinant matrixes to differentiate levels of squish

|   |   |   |
|---|---|---|
|![Rank1](../resources/la_rank_01.png)|![Rank2](../resources/la_rank_02.png)|![Rank3](../resources/la_rank_03.png)|

* **Column Space** is the set of all possible outputs for a matrix

![Column Space](../resources/la_column_space.png)

* "[Rank] is the number of dimensions in the column space."


#### Null Space

* **Null Space** is the set of vectors that get squished into the origin when a matrix lowers rank

|   |   |
|---|---|
|![Pre Null Space](../resources/la_null_space_pre.png)|![Post Null Space](../resources/la_null_space_post.png)|
