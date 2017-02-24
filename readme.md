2D Affine Transformation Matrix
-------------------------------

An affine transformation matrix (3x3) class for JavaScript that performs
various transformations such as rotate, scale, translate, skew, shear, add,
subtract, multiply, divide, inverse, decomposing and more (full HTML
documentation is included).

It's primarily intended for situations where you need to track or create
transforms and want to apply it permanently/manually to your own points
and polygons.

The matrix can optionally synchronize a canvas 2D context so that the
transformations on the canvas matches pixel perfect the local
transformations of the Matrix object. It can be used to synchronize a
DOM element using the toCSS()/toCSS3D() method.

No dependencies. Node support.


Install
-------

Download zip and extract to folder.

git via HTTPS:

    $ git clone https://github.com/epistemex/transformation-matrix-js.git

git via SSH:

    $ git clone git@github.com:epistemex/transformation-matrix-js.git

Using Bower:

    $ bower install transformation-matrix-js

Using NPM

    $ npm install transformation-matrix-js


Usage
-----

Just include the script and create a new instance:

    var matrix = new Matrix([context]);

You can supply an optional canvas 2D context as argument, which will be
synchronized with the transformations that are applied to the matrix
object.

Using it with Node - use npm to install the package first, then:

    var demo = require("transformation-matrix-js");
    var matrix = new demo.Matrix();

Some of the methods:

    matrix.interpolateAnim();           // decomposed interpolation
    matrix.toString();
    matrix.toJSON();
    matrix.toCSS();
    matrix.toCSS3D();
    matrix.toArray();
	matrix.toTypedArray();				// binary array
    matrix.rotate(angle);    		    // angle in radians
    matrix.rotateDeg(angle);   		    // angle in degrees
    matrix.rotateFromVector(x, y);      // use a vector to set angle
    matrix.translate(x, y);
    matrix.translateX(x);
    matrix.translateY(y);
    matrix.scale(sx, sy);
    matrix.scaleX(sx);
    matrix.scaleY(sy);
    matrix.scaleU(f);                    // scale both x and y
    matrix.shear(sx, sy);
    matrix.shearX(sx);
    matrix.shearY(sy);
    matrix.skew(ax, ay);                // angle in radians
    matrix.skewX(ax);
    matrix.skewY(ay);
    matrix.transform(a, b, c, d, e, f);
    matrix.setTransform(a, b, c, d, e, f);
    matrix.divide();                    // divide matrix on another matrix
    matrix.divideScalar();              // divide matrix by scalar value
    matrix.inverse();
    matrix.decompose([lu]);             // BETA decompose matrix using QR or LU
    matrix.determinant();               // get determinant of current matrix
	matrix.reset();
    matrix.clone();
    matrix.isInvertible();
	matrix.isValid();
    matrix.reflectVector(x, y)         // reflects vector on normal (=current x-axis);
    matrix.concat(childMatrix)

Get current transform matrix properties:

    var a = matrix.a;	// scale x
    var b = matrix.b;	// shear y
    var c = matrix.c;	// shear x
    var d = matrix.d;	// scale y
    var e = matrix.e;	// translate x
    var f = matrix.f;	// translate y

(also see `decompose()`).

Apply to a point:

    var tPoint = matrix.applyToPoint(x, y);

Apply to an Array with point objects or point pair values:

    var tPoints = matrix.applyToArray([{x: x1, y: y1}, {x: x2, y: y2}, ...]);
    var tPoints = matrix.applyToArray([x1, y1, x2, y2, ...]);
    var tPoints = matrix.applyToTypedArray(...);

or apply to a canvas context (other than optionally referenced in constructor):

    matrix.applyToContext(myContext);

Get inverse transformation matrix (the matrix you need to apply to get back
to an identity matrix from whatever the matrix contains):

    var invmatrix = matrix.inverse();

or

    var invmatrix;

    if (matrix.isInvertible()) {                  // check if we can inverse
        invmatrix = matrix.inverse();
    }

You can interpolate between current and a new matrix. The function
returns a new matrix:

    var imatrix = matrix.interpolate(matrix2, t);  // t = [0.0, 1.0]
    var imatrix = matrix.interpolateAnim(matrix2, t);

The former does a naive interpolation which works fine with translate
and scale. The latter is better suited when there is for example rotation
involved to avoid "flipping" (and is what the browsers are using) utilizing
decomposition.

Check if there is any transforms applied:

    var status = matrix.isIdentity();              // true if identity

Check if two matrices are identical:

    var status = matrix.isEqual(matrix2);          // true if equal

Reset matrix to an identity matrix:

    matrix.reset();

Methods are chainable:

    matrix.rotateDeg(45).translate(100, 120);     // rotate, then translate

To synchronize a DOM element:

    elem.style.transform = matrix.toCSS();        // some browsers may need prefix

See documentation for full overview and usage.


Contributors
------------

- Ken "Fyrstenberg" Nilsen (creator) (https://github.com/epistemex)
- Leon Sorokin (https://github.com/leeoniya)
- Henry Ruhs (https://github.com/redaxmedia)

See Change.log for details.


License
-------

Released under [MIT license](http://choosealicense.com/licenses/mit/). You can use this class in both commercial and non-commercial projects provided that full header (minified and developer versions) is included.

*&copy; 2014-2016 Epistemex*

![Epistemex](http://i.imgur.com/wZSsyt8.png)
