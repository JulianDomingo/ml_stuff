## Image Classification

#### Background
* Large focus on tuning + tweaking CNNs for purpose of optimizing
    classification performance
* Why have CNNs only become so popular over the last few years?
    * More compute power: Moore's Law, GPUs
    * Larger data sets

#### Introduction
* Predetermined set of labels
* Challenges w/ image classification algorithms
    * Semantic gap with images (computer just sees a grid of rgb numbers)
    * Viewpoint variation -> all pixel values change
    * Illumination
    * Deformation
    * Occlusion (not all of the object is visible)
    * Background clutter
    * Intraclass variation -> different appearances despite same object type
* No obvious way to hard-code a classification task
* Data-driven Approach
    * Gather: Collect set of images w/ labels (train set)
    * Train: Use ML to output a model
        * train(X, y) where **X** is training data set (each row is example) and **y**
            is correct label of corresponding row in **X**
    * Predict: Evalute model on new (unseen) images (test set)
        * predict(X) where **X** is N rows of unlabeled data. Outputs
            1-dimensional column of resultant predictions

#### Nearest Neighbor
* Memorize all data and labels
* Predict class as label of the most similar training image (L1 / hamming
    distance)
* Bad runtime:
    * **Fast** at train time, **Slow** at test/predict time
    * Want the opposite -> when you deploy model, want it to be fast for user
        (i.e. Google Lens for image recognition)
* Problems
    * Carved out "regions" when visualizing Nearest Neighbors could potentially
        have a lot of labeling errors caused from outlier points from training set data.
        * Imagine an outlier point with label X on a 2D grid located within the
            region of points carved out by label Y - the outlier point would
            form an "island" inside of region Y, so training points close to
            this outlier would mistakenly get labeled as X even though they are
            likely label Y.
* Optimizations
    * **K-Nearest Neighbors**
        * Copy label not just from **one** (closest) neighbor, but instead **k**
            closest neighbors, and predict label based on **majority vote** of
            those **k** neighbor labels
        * Visually, "smooths" out decision boundaries / carved labeling regions
        * How should we be comparing our points?
        * Topology differences:
            * L1 (Hamming) distance:
                * Changing coordinate frame changes distance
                * More natural when vector features have meaning (i.e. if data
                    points are employees, then features like salary, years @
                    company provide concrete inferences)
            * L2 (Euclidean) distance
                * Changing coordinate frame doesn't change distance
                * More natural for ambiguous vectors
        * Applicable to many areas
            * NLP: distance between paragraphs / sentences
    * Problems
        * Prone to Curse of dimensionality
            * As number of dimensions increase, number of training samples / points needed to
                densely cover the space / accurately grows exponentially w.r.t. to the # of
                dimensions (similar to combinatorial problems)

#### Hyperparameters
* Things like the value of **k** or **L1 vs L2** in KNN is an example of a hyperparameter
    * Choices about the algorithm that **we set** rather than **learn**. Very
        problem-dependent on choosing appropriate hyperparameters
* How to pick hyperparameters
    * Train/test split? -> no idea how algorithm will perform on new / unseen data
    * Split data in train/validation/test split? ->
        * Train algorithm with varying hyperparameters on training set
        * Evaluate best hyperparameters based on which perform the best on validation set
        * Finally, take best performing classifier with evluated hyperparameters
            from validation set and use it for predictions (test set)
    * Cross-Validation
        * Popular / effective for **small** data sets, not used often for deep
            learning in practice due to size of data sets + computational
            expenses
        * Split data into folds, try **EACH** fold as validation set and **average**
            the results
            * Common for 5 or 10 fold CV
    * Assumption with deep learning is **data sets are drawn from roughly the
        same probability distribution**, so test data is often representative of
        data seen "in the wild."
        * Cases where above isn't true is a data set curator / creation issue
            * Good way to avoid this is by randomly partitioning data
    * **Good to make plots for CV accuracy as hyperparameter ranges vary**
