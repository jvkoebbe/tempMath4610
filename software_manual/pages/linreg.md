# Math 4610 Fundamentals of Computational Mathematics Software Manual Template File
This is a template file for building an entry in the student software manual project. You should use the formatting below to
define an entry in your software manual.

**Routine Name:**           linreg

**Author:** Joe Koebbe

**Language:** Java. The code can be compiled javac.
For example,

    javac LinearRegression.java

will produce a class file to run in a Java Runtime executable. To run the code use:

    java LinearRegression

**Description/Purpose:** This routine will compute the single precision value for the machine epsilon or the number of digits
in the representation of real numbers in single precision. This is a routine for analyzing the behavior of any computer. This
usually will need to be run one time for each computer.

**Input:** There are no inputs needed in this case. Even though there are arguments supplied, the real purpose is to
return values in those variables.

**Output:** This routine returns a single precision value for the number of decimal digits that can be represented on the
computer being queried.

**Usage/Example:**

The routine has two arguments needed to return the values of the precision in terms of the smallest number that can be
represented. Since the code is written in terms of a Fortran subroutine, the values of the machine machine epsilon and
the power of two that gives the machine epsilon. Due to implicit Fortran typing, the first argument is a single precision
value and the second is an integer.

      call smaceps(sval, ipow)
      print *, ipow, sval

Output from the lines above:

      24   5.96046448E-08

The first value (24) is the number of binary digits that define the machine epsilon and the second is related to the
decimal version of the same value. The number of decimal digits that can be represented is roughly eight (E-08 on the
end of the second value).

Implementation/Code: The following is the code for smaceps()

```
import java.io.*;
import java.util.Random;

public class LinearRegression extends Object
{
  //
  // this method will do a standard linear regression on the input data
  // ------------------------------------------------------------------
  //
  double [] linreg(double [] x, double [] y)
  {
    //
    // determine the number of entries in the two data arrays
    // ------------------------------------------------------
    //
    int n = x.length;
    double cval, rval;
    double [] output = new double[2];
    //
    // initialize the matrix variables
    // -------------------------------
    //
    a11 = 0.0;
    a12 = 0.0;
    a21 = 0.0;
    a22 = 0.0;
    b1 = 0.0;
    b2 = 0.0;
    //
    // loop over data
    // --------------
    //
    a11 = (double) n;
    for(int k=0; k<n; k++)
    {
      a12 = a12 + x[k];
      a22 = a22 + x[k] * x[k];
      b1 = b1 + y[k];
      b2 = b2 + x[k] * y[k];
    }
    a21 = a12;
    //
    // write out the solution for the system using the 2x2 formula
    // ------------------------------------------------------------
    //
    detval = a11 * a22 - a12 * a21;
    cval = ( a22 * b1 - a12 * b2 ) / detval;
    rval = ( - a21 * b1 + a11 * b2 ) / detval;
    //
    // return the values
    // -----------------
    //
    output[0] = cval;
    output[1] = rval;
    return output;
    //
  }

  public static void main(String args[]) {
    LinearRegression lr = new LinearRegression();
    Random r = new Random();
    int nd = 101;
    double dx = 1.0 / ((double) nd);
    double [] x = new double[nd];
    double [] y = new double[nd];
    for(int i=0; i<nd; i++)
    {
      x[i] = ((double) i) * dx; 
      y[i] = 2.0 * x[i] * x[i] + 0.001 * r.nextDouble();
    }
    double [] output = lr.linreg(x, y);
    System.out.println("Constant value:    " + output[0]);
    System.out.println("Slope value:    " + output[1]);
    //
  }

  //
  // local variables
  // ---------------
  //
  public double a11, a12, a21, a22;
  public double b1, b2;
  public double detval = 0.0;

}

```

Last Modified: September/2017
