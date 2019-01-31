#### Linear Classification
* Can think of CNNs as compositions of linear classifier layers

#### A Parametric Model for Image Classification Use Case
* 2 different components: image matrix **x** and parameters/weights **W**
* **f(x, W)** spits out probability scores for each possible label
    * More efficient memory-wise, as only need parameters as opposed to entire
        input images
* Example
    * f(x, W) = Wx + b
        * Uses dot/inner product of unraveled input matrix image and parameter
            weight matrix
        * b is bias vector
    * Once you train the linear classifier model, can "roll / undo unravel" each
        row of **W** to visually see what the classifier sees for each label
        * Problem:
            * Linear classifier only uses / allowed to use a single template, which averages out
                all training samples, as the basis for classification
        * Solution:
            * Once we reach CNNs, no longer have these restrictions
    * Visually through high-dimensional POV, linear classifier seeks to place linear decision boundaries within plane to separate a label X from all other labels
        * Issues with **multimodal data** (one class/label that can appear in
            different regions of space)

#### Best Strategies for Choosing the Best **W**
