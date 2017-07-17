# Consistently faster and smaller compressed bitmaps with Roaring
[Source](https://arxiv.org/pdf/1603.06549.pdf)

## Introduction
- bitmaps allow bit level parallelism by computing set unions (OR), intersections (AND) and differences (AND NOT). More complicated operations can be implemented as bitwise operations.
- can support threshold top-k queries (see "Compressed bitmap indexes: beyond unions and intersections")
- problem: if set density is low, bitmaps loose their compression edge. 
 - A solution is to use RLE: provides good compression and fast decoding.
 - a variation of RLE are hierarchical bitmaps (see: "Hierarchical bitmap index: an efficient and scalable indexing technique for set-valued attributes")
- problem: RLE does not allow random access
- objectives for roaring indexes:
 - fast random access
 - optimize for modern processors: superscalar execution, few branches, new instructions (see [POPCNT](https://en.wikipedia.org/wiki/SSE4) )
 - good compression over a wide range of cases
 - cache friendly
- based on RidBIT implementation: 2-level tree with 2 types of containers: arrays + bitmaps
 - need to decide if to use array or bitmap dynamically: not a downside since most processors have an instruction to compute Hamming weight (1s in word) + well chosen algorithms (container prediction (if the sum of their cardinalities exceeds 4096, we use a bitmap, otherwise we choose an array), galloping intersection)
 - add a third container, to solve poor compression for data made of runs of consecutive values. Given a run (e.g., [10, 1000]), we store the starting point (10) and its length minus one (990). By packing the starting points and the lengths in pairs, using 16 bits each, we preserve the ability to support fast random access by binary search through the coded runs. 

## Roaring bitmap
Container structure:
- bitmap container:  object made of 1024 64-bit words (using 8 kB) representing an uncompressed bitmap, able to store all sets of 16-bit integers. The container can be serialized as an array of 64-bit words. We also maintain a counter to record how many bits are set to 1.
- array container: object containing a counter keeping track of the number of integers, followed by a packed array of sorted 16-bit unsigned integers. It can be serialized as an array of 16-bit values.
- run container: packed array of pairs of 16-bit integers. The first value of each pair represents a starting value, whereas the second value is the length of a run. Used only when same data cannot be represented with same or less memory with one of precedent containers.

## Logical operations
- union and intersection: use of galloping search, which requires random access but does not degrade performance since all containers fit into CPU cache.
- heap usage to select which containers should be combined and how
- operations between bitmap, array and run containers:
 - bitmap vs. bitmap: for intersection, we compute cardinality: if exceeds 4096, materialize into new bitmap, othwerwise into array container. Union is calculated as OR over both bitmaps
 - bitmap vs. array: intersection created into array of same size as array used for intersection. Union created into bitmap iterating over values in array and setting 1s.
 - array vs. array: intersection is always a new array, with the minimum cardinality of both arrays. For unions, if the cardinality of both arrays is less than 4096, values are merged into a new array container. Otherwise, a bitmap is created and values set to 1s.
- run vs. run: intersection done creating new run container with capacity to sum both containers. For unions, an empty one is created and values added. Eventually the run container is converted into a bitmap container, if too many are used.
- run vs. array: intersection always outputs an array container. Union requires to output into array or bitmap container based on result cardinality.
- run vs. bitmap: intersection requires computing run cardinality: if less than 4096, an empty array is created, otherwise a bitmap is used.

Some operations can be executin in-place: require no additional memory and improve data locality.

## Conclusion
We have shown how a hybrid bitmap format, combining three container types (arrays, bitmaps and runs) in a two-level tree could surpass competitive implementations of other popular formats (Concise, WAH, EWAH), being up to hundreds of times faster. For analytical applications, where the bitmaps are not constantly updated, and where we can afford to sort the data prior to indexing, applying run compression to the Roaring format is particularly appealing. The new format has been adopted by existing systems such as Apache Spark, Apache Kylin and Druid.

# Other links of interest:
- [Bit map index and SQL](https://richardstartin.com/2017/01/09/how-a-bitmap-index-works/)
- [Pilosa data model](https://www.pilosa.com/docs/data-model/): opensource distributed bitmap index. 

