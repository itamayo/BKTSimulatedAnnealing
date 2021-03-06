## Bayesian Knowledge Tracing Parameter Fitting by Simulated Annealing

This code is based on the original [BKT Brute Force](http://www.columbia.edu/~rsb2162/BKT-BruteForce.zip) code from Baker, Corbett, and Aleven (2008).  In that code, BKT parameters were fit by trying every combination of the four BKT parameters `Lzero`, `Guess`, `Slip`, and `T` on a fine-grained grid, and reurning the combination which resulted in the best sum of squared residuals (`SSR`) on predicting the student's answers.

__Note__: _This class expects a tab-delimited input file, sorted by Skill and then by Student -- see the included [TestData.txt](TestData.txt) (the original test file from Baker et al. without modification).  The name of the input file is passed as a command-line argument; e.g._ `java computeKTparams_SA TestData.txt`.

This code modifies that behavior by fitting the parameters using simulated annealing.  Initial, random guesses are selected for the four parameters, and the root mean squared error (`RMSE`) is calculated.  A Monte Carlo algorithm is carried out by successively randomly changing the parameters by small amounts, and accepting or rejecting these changes based upon the Metropolis criterion:

```java
P(accept) = Math.exp((oldRMSE-newRMSE)/temp)
```

In this equation, `temp` is a virtual temperature, which is slowly decreased until the RMSE stops changing (or until the maximum number of steps, which is set to `1,000,000` by default).  At all times, the set of parameters resulting in the lowest `RMSE` is retained: while the Monte Carlo algorith allows the `RMSE` to increase to avoid getting trapped in local minima, we are interested in the global minimum.  For more details, see Miller, Baker, and Rossi (in press). 

This tool is copyright William Miller, Ryan Baker, and colleagues -- it is free for any non-commercial or research use. Please contact me before using for any commercial use. This code is NOT supported. Use it at your own risk, and make sure to check that data is sorted properly. You are welcome to re-distribute this code as long as proper credit is given. If you use this code for a published paper, please cite Miller _et al._ (2014).

References:  

1.	Baker, R.S.J.d., Corbett, A.T., Aleven, V. (2008) [More Accurate Student Modeling Through Contextual Estimation of Slip and Guess Probabilities in Bayesian Knowledge Tracing](http://dl.acm.org/citation.cfm?id=1426036). _Proceedings of the 9th International Conference on Intelligent Tutoring Systems_, 406-415.
2. Miller, W. L., Baker, R.S. and Rossi, L.M. (2014) [Unifying Computer-Based Assessment Across Conceptual Instruction, Problem-Solving, and Digital Games](http://dx.doi.org/10.1007/s10758-014-9225-5). _Technology, Knowledge and Learning_. 165-181. ([preprint](https://github.com/wlmiller/wlmiller.github.io/raw/master/files/TKNL_final_full.pdf))
