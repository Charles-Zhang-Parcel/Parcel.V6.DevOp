# High-Level Design Notes

Parcel is intended for non-programmers while with a focus to "technical-design" perspective. The main problem it tries to solve is for teams with very liquid personnel and a need for maintainable automated software solutions without the involvement of strong IT support. 

The major inspiration for Parcel is Houdini, along with many other node-based content editing tools. Due to the nature of 2D graphical node-based representation, Parcel's data is inherently unfriendly to version control and maybe subject to potential limits in scalability - however this problem is alleviated internally through unique asset ID per document; Even so, it's recognized that for those well versed in the art of programming, it might be more efficient to write well-organized codes instead of using Parcel for sophisticated software solutions.

## Topics

* **File Format**: For information on file format, see [File Format](./File%20Format).
* **Cache**: See [Caching](/Caching)