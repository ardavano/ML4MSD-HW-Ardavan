# Assignment 3 - Reading Summary: Machine Learning Refined

**Author:** Ardavan Mehdizadeh  
**Course:** ML4MSD - Homework 2  
**Date:** October 6, 2025

## Introduction

For this assignment, I worked through several chapters from "Machine Learning Refined" by Watt, Borhani, and Katsaggelos. The goal was to understand concepts that either weren't covered in lecture or were covered only briefly. I focused on chapters dealing with extensions of basic regression and classification methods, as well as practical topics like model selection. Overall, these readings helped fill in gaps from class and gave me a better understanding of how the methods we've been using actually work under the hood.

## Chapter 5.6: Multi-Output Regression

Chapter 5.6 extends standard linear regression from predicting a single scalar output to predicting multiple outputs simultaneously. Instead of just predicting one value like band gap, you could predict multiple material properties at once using vector-valued outputs. The math is actually pretty straightforward, you just use a weight matrix W instead of a weight vector w, where each column of W corresponds to one output dimension. The cost functions extend naturally using vector norms, so the Least Squares cost uses the squared L2 norm of the error vector for each point.

What I found interesting is that each output dimension can be optimized independently since the weights don't interact between outputs. This means you could train separate models for each output and get the same result, but it's more efficient to do it all at once with the matrix formulation. This directly relates to materials science applications, if I wanted to predict both band gap and conductivity for materials, I could use one multi-output model instead of training two separate models. The chapter emphasized that the Python implementation is almost identical to regular regression, just handling matrix operations instead of vectors.

## Chapter 6.5: Support Vector Machines

The SVM chapter introduced the idea of finding the "best" decision boundary by maximizing the margin between classes. There are two versions: hard-margin SVM assumes the data is perfectly separable, while soft-margin SVM allows for some misclassified points. The hard-margin version tries to maximize the distance between the decision boundary and the nearest points from each class (the support vectors). You do this by minimizing the length of the normal vector subject to the constraint that all points are classified correctly.

The practical reality is that real data is rarely perfectly separable, so soft-margin SVM is what people actually use. It adds a regularization parameter λ to handle noisy or overlapping data. Here's what surprised me: for non-separable data, soft-margin SVM often gives exactly the same results as logistic regression or the perceptron. The chapter showed mathematically that the soft-margin SVM cost is really just regularized logistic regression in disguise. This explains why SVMs were popular historically for their theoretical properties (the maximum margin concept is elegant), but in practice they don't usually outperform simpler methods like logistic regression on messy real-world data. The "margin" concept only really matters when data is perfectly separable, which almost never happens in practice.

## Chapter 6.6: The Categorical Cross Entropy Cost

This was a shorter chapter that showed you can represent binary classification labels as one-hot vectors instead of numerical values. So instead of using +1 and -1, you could use [1,0] and [0,1]. The chapter derives the cost function for these categorical labels and proves it's mathematically equivalent to the regular cross entropy we've been using. The point is that the specific representation of labels doesn't fundamentally matter, whether you use numbers or categorical one-hot vectors, you end up solving the same optimization problem.

I hadn't really thought about this flexibility before. In practice, this matters when you're using ML frameworks like TensorFlow or PyTorch, where you see functions named "binary_crossentropy" and "categorical_crossentropy." Now I understand they're solving the same underlying problem, just accepting different input formats. The chapter also mentioned that one-hot encoding isn't just for multi-class problems, you can use it for binary classification too, which helps unify the mathematical notation across different types of classification tasks.

## Chapter 6.7: Which Approach Produces the Best Results?

This chapter addresses a practical question: which classification method should you use, logistic regression, perceptron, or SVM? The answer is refreshingly honest: they're all so closely related that they typically give comparable results. Since they all minimize the same or very similar cost functions (softmax/cross entropy with maybe slightly different regularization), you shouldn't expect huge performance differences.

The practical takeaway is that you don't need to agonize over which method to pick. Just use whichever you're comfortable with, or if you have time, try multiple approaches and use whichever performs best on your specific dataset. This was actually reassuring, sometimes in ML courses you get the impression that picking the "right" algorithm is critical, but for basic linear classification, the method matters less than good feature engineering and proper validation. It also explains why in our homework we saw similar performance from different approaches.

## Chapter 6.8: Classification Quality Metrics

This chapter covers how to evaluate classification models properly. The basic metric is accuracy, which is just the percentage of correct predictions. But there's an important practical issue: the cost function value doesn't perfectly track with the number of misclassifications. The chapter showed examples where the cost function decreases but misclassifications stay the same or even increase temporarily. This happens because our cost functions (like softmax) are just smooth approximations to the discrete step function we really care about. The practical implication is that after training, you should pick the model with the best accuracy, not necessarily the one with the lowest cost function value.

The chapter also introduced balanced accuracy, which is crucial for imbalanced datasets. If you have 99% of one class and 1% of another, you could get 99% accuracy by just always predicting the majority class. Balanced accuracy fixes this by computing accuracy on each class separately and averaging them. So in that example, you'd get 100% on the majority class but 0% on the minority class, giving 50% balanced accuracy, which correctly reflects that you're completely missing one class.

The confusion matrix concept ties everything together, it's a 2x2 table showing true positives, false positives, true negatives, and false negatives. From this you can compute various metrics. The chapter also explained confidence scoring using the sigmoid function applied to the distance from the decision boundary. Points far from the boundary get high confidence scores (close to 0 or 1), while points near the boundary get low confidence (close to 0.5). This is useful for real applications where you might want to flag low-confidence predictions for manual review.

## Chapter 6.9: Weighted Two-Class Classification

Chapter 6.9 tackles a really practical problem: how to handle imbalanced datasets. The idea is to assign different importance weights to different data points. You multiply each point's contribution to the cost function by a weight β. These weights are fixed (not learned), you set them before training based on class membership.

The common approach for imbalanced data is to weight points inversely proportional to their class size. If you have 99 healthy patients and 1 sick patient, you'd weight the sick patient 99 times more heavily than each healthy patient. This prevents the model from just classifying everything as the majority class to achieve high overall accuracy. Without weighting, a model might learn to always predict "healthy" and get 99% accuracy, which is useless for actually detecting disease.

This concept applies to tons of real-world problems: fraud detection where most transactions are legitimate, spam filtering where most emails aren't spam, disease detection where most people are healthy. The practical formula is simple: for class with N+ members, set weight to N/N+, and similarly for the other class. The weighting doesn't change the optimization algorithm, you still use gradient descent or Newton's method, it just changes the cost function to reflect that misclassifying a minority class member is much worse than misclassifying a majority class member.

## Chapter 7.3: Multi-Class Classification and the Perceptron

This chapter extends binary classification to multiple classes (more than 2). Instead of training classifiers separately and combining them afterward (the One-versus-All approach), you can train all classifiers simultaneously. The key idea is the fusion rule: for each point, pick whichever classifier gives the highest score. The multi-class perceptron cost function directly optimizes all classifiers at once to satisfy this fusion rule as often as possible.

The chapter then introduces the multi-class softmax cost, which is a smoothed version that's easier to optimize. It replaces the max function with log-sum-exp, which is differentiable and allows you to use Newton's method. Both the multi-class perceptron and softmax need regularization (usually λ around 10^-5) to keep weights from growing too large. An important detail: when you only have 2 classes (C=2), these multi-class formulations reduce exactly to the regular two-class versions we've seen before.

The chapter emphasized that softmax and cross-entropy are actually just different names for the same thing, which had been confusing me before. The Python implementation uses matrix operations instead of for-loops to make things faster. The key insight is that by training all classifiers jointly instead of separately, the weights can "interact" during optimization to minimize total misclassifications across all classes, which often works better than training them independently.

## Chapter 7.4: Which Approach Produces the Best Results?

This chapter compares One-versus-All (OvA) versus multi-class softmax for multi-class problems. The main finding is that multi-class softmax generally performs better because it trains all classifiers together to minimize overall misclassifications. OvA trains each classifier separately, one class versus all others, which can fail badly in certain scenarios.

The chapter showed a concrete example where OvA completely missed a minority class that was surrounded by other classes. When you frame it as "khaki class versus everyone else" and khaki is heavily outnumbered, the optimal solution for that subproblem is to just classify everything as "not khaki." But when you train all classifiers jointly with softmax, the model can balance all the classes properly because it's directly minimizing total errors across all classes simultaneously.

The chapter connected this back to the weight matrix formulation, both approaches use the same weight matrix W, but OvA tunes each column independently while softmax tunes them all together. This joint optimization is why modern deep learning frameworks default to using softmax/cross-entropy for multi-class problems rather than training separate binary classifiers. The OvA approach is "myopic", each classifier only sees its own subproblem, while softmax sees the whole picture from the start.

## Chapter 11.4: Naive Cross-Validation

This chapter explains the basic approach to model selection: naive cross-validation. The process is straightforward, split your data into training and validation sets (like 66% train, 33% validation), then train a bunch of models with increasing complexity and pick whichever has the lowest validation error. You might train polynomials of degree 1, 2, 3, and so on, fully optimizing each one on the training data.

The chapter explained the characteristic U-shaped validation error curve. As models get more complex, training error always decreases because more complex models can fit the training data better. But validation error first decreases then starts increasing again. The minimum point is the "sweet spot" that balances underfitting and overfitting. This is called solving the bias-variance tradeoff.

The problem with naive cross-validation is that it's computationally expensive, you have to fully train every model you test, and it gives you a coarse search. Jumping from K to K+1 units is a big capacity jump, so you might skip over the ideal model complexity. The chapter used this great "capacity dial" versus "optimization dial" visualization. Naive CV turns the capacity dial all the way through while keeping optimization maxed out, which is expensive and coarse-grained.

Better approaches would adjust the optimization dial instead to get finer control over model complexity, though the chapter didn't go into detail on those methods. This directly relates to our ridge regression homework where we used different alpha values. We were essentially doing a form of cross-validation, but instead of changing model structure (the capacity dial), we were controlling complexity through regularization. The chapter made me realize why we saw that pattern where test error first decreased then might increase with very large alpha values, we were moving along that U-shaped validation curve.

## Overall Reflections

Working through these chapters really helped me see how interconnected different ML methods actually are. The biggest insight was understanding that many algorithms that seem different are really just variations on the same underlying optimization problems. Support Vector Machines sound fancy and different from logistic regression, but with noisy data they're essentially the same thing, just regularized logistic regression with a different perspective. Similarly, the multi-class perceptron and softmax are smoothed versions of each other, and categorical cross-entropy is just regular cross-entropy with different label encoding.

Another key realization was understanding the difference between what we optimize (the cost function) and what we really care about (misclassifications or accuracy). The cost functions we use are smooth approximations that make optimization possible, but they don't perfectly track with actual performance. This is why you need to pick the model with the best validation accuracy rather than lowest cost function value, and why proper evaluation with validation sets is so critical.

The practical chapters on weighted classification and model evaluation metrics were especially valuable. Most ML courses focus heavily on the algorithms themselves, but knowing how to handle imbalanced datasets and properly evaluate models is just as important in real applications. The balanced accuracy concept and the weighting scheme for imbalanced data are things I'll definitely use in any real project.

The cross-validation chapter tied everything together by explaining why we can't just trust training error. The U-shaped validation curve makes perfect sense now, models can fit training data perfectly while being useless on new data. This connects directly to our homework where we tested different alpha values for ridge regression. We were doing a form of model selection, searching for the right amount of regularization to balance fitting the training data with generalizing to new data.

Overall, these readings filled in a lot of gaps from lecture and gave me a much better intuition for why these methods work the way they do. Understanding that many "different" algorithms are really the same thing helps demystify ML and makes it easier to learn new methods in the future, since I can relate them back to these fundamental frameworks we've covered.

## References

Watt, J., Borhani, R., & Katsaggelos, A. K. *Machine Learning Refined: Foundations, Algorithms, and Applications* (2nd Edition). Cambridge University Press.

Free online version: https://github.com/neonwatty/machine-learning-refined