# Face Orientation Test
To confirm the implementation details of the face orientation in T8code, specifically cross-facet face corner numbering ordering consistency, allowing for modulo based face orientation encoding, we write a test. The test copies the active implementation to find the face corner number of a neighbour (and thus neighbour element corner number in general) found inside ```Check_Corner_Face_Neighbour_Corner_Canonisation()```. We then use a rough geometric comparison on a 3-dimensional hypercube comprised of tetrahedra of the two equivalent vertices to determine if the results are consistent, we do so for a range of faces of an element (note that comparisons are limited to a single tree to prevent previously observed discrepancies between tree coordinate systems). 

A possible point of concern is that when geometrically evaluating points using the ```t8_forest_element_coordinate()``` function, the corner number argument is specified to require Z-order, while other corner related functions do not. This may break the test. I will investigate the source code to find any hints as to the equivalence or possibly workarounds related to this issue. From the source code it does not appear like the Z-order is significant.

# Debugging and ```t8_element_t``` Type Incompleteness
Debugging has begun with the "completion" of the foundations of the face orientation test and vertex equivalence disjoint set union implementation. An error has again occurred regarding ```t8_element_t``` status as an incomplete type, not allowing such an object to be allocated. This error has occurred in relation to the ```t8_forest_element_face_neighbor()```. A variable was instantiated via ```t8_element_t neighbour_element;``` and then passed to the function by address, the instantiation line produces an error. Examining the documentation appears a bit odd at first "*inout On input an allocated element of the scheme of the face_neighbors eclass. On output, this element’s data is filled with the data of the face neighbor. If the neighbor does not exist the data could be modified arbitrarily.*" Considering possible meaning, I come t believe that the instantiation of the neighbour element variable should instead begin with a ```t8_element_t* neighbour_element_ptr;``` declaration which is then assigned to some allocated memory where the neighbour element will be output. It appears the function ```t8_element_new()``` will be the solution here.

> [!NOTE] 
> ```t8_element_destroy()``` is the matches deallocation function.

# Face Orientation Test Results
Note that with logging, the face orientation test must be run with debug mode enabled. 

Initial results show that the corner equivalence algorithm fails, though in a perfectly deterministic way. Additionally, it appears only one side is resulting in instance of corner equivalence failures.

Correction, after including success instance detection, it appears only four comparisons are ever made. We should determine if these are of a specific face, corner, or combination thereof.

It appears only one face is iterated over, however, this may be a result of the position of the chosen element. Tweaking the chosen starting element to have more faces in contact with its tree provides significantly more information. A pattern regarding the current element face numbers seems to appear, smaller current element face numbers appear to produce more failures, while higher values appear to produce less failures, this encourages me to explore the ```main_face``` decision making algorithm.
