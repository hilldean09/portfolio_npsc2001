# Topologically Aware Global Vertex Indexing Algorithm
The following algorithm was presented by Dr. Alberto Martin after an online meeting where flaws in the previous algorithm was discovered.

```
Select the first element, and assign the global vertex identifiers 1, 2, and 3 to its three vertices.

Add the first element to a set of elements S for which all of their vertices have already been numbered

next_global_vertex_id = 4

Queue the first element into Q, with Q being a queue of elements

While Q not empty:

    cur_element = Dequeue(Q)

     Go over the local facets of cur_element

            neig_element = extract neighbour of cur_element across current local_facet

            If not neig_element in S

                  1. Transfer the global IDs of the vertices of cur_element to the corresponding ones in neig_element

                  while taking into account that the orientation of the matching facets from the perspective of

                  either element may not match (one might be flipped w.r.t. each other)

                 2. Assign the global vertex id  next_global_vertex_id to the remaining vertex of cur_element

                 3. Increment next_global_vertex_id

                 4. Add neig_element to S

                 5. Queue neig_element into Q
```

Note that an alternative is using the previously discussed algorithm with the addition of a vertex-centric depth-first-search algorithm. Note that this alternative is less memory intensive (and allows easier per-tree parallelism).
```
do_process_corner_bool_array

# Iterate over every corner of every element of every tree checking if the corner has been processed, storing it if it hasn't

for tree in forest.trees:
	for element in tree.elements:
		for corner in element.corners:
			if not has_corner_been_processed(element, corner):
				store_corner(element, corner)
```

We define the ```has_corner_been_processed()``` function with the following:
```
# Depth first search of all elements touching the given corner
def has_corner_been_processed(start_element, corner):
	output = False
	
	dfs_stack = new_empty_stack()
	dfs_stack.push(start_element)
	visited_element_indexes = new_empty_list()
	
	# Depth-First-Search algorithm
	# Checking if the output has remained false
	while dfs_stack.not_empty() and not output:
		
		cur_element = dfs_stack.pop()
		if not get_element_index(cur_element) in visited_element_index:
		
			# Checking if the element has been processed, if it has this indicates that the corner has been processed
			if has_element_been_processed(cur_element, start_element):
				output = True
			
			# Searching through facets which contain the corner of interest
			for corner_facet in corner.facets:
				neighbour_element = get_face_neighbour( element, corner_facet)
				if not get_element_index( neighbour_element) in visited_element_indexes:
					dfs_stack.push(neighbour_element)
	
	return output
```

We define the ```has_element_been_processed()``` function as checking whether the current element's element index is less than the starting element's index or if the current element lies in a tree with a lower tree index than the current element.
```
def has_element_been_processed(cur_element, start_element):
	output = False
	
	# Note that the case where the tree index of the current element is greater than the tree index of the starting element is implicitly handled
	if get_tree_index( cur_element ) == get_tree_index( start_element ):
		if get_element_index( cur_element ) < get_element_index( start_element):
			output = True
			
	else if get_tree_index( cur_element ) < get_tree_index( statr_element ):
		# Considering the trees have been iterated over, a tree of a lower index has always already been processed.
		output = True
	
	return output
```
Please note that the algorithm above does not get into the specifics of working with the T8code interface but all functionality assumed in the above has been confirmed to exist in T8code.

# Getting the Element Index of a ```t8_element_t``` Instance
The element index of a ```t8_element_t``` instance appears to be an elusive value to find initially (in the context of forests), however, a function to do so exists in the ```t8_element_array_...``` group of functions, only requiring the ```t8_element_t``` instance, the element array (which can be obtained from a forest), and the level of the element.

# Algorithm Comparison
For ease of reading I will dub Dr. Martin's algorithm (see above) as the "global breadth first search" (GBFS) algorithm and my algorithm as the "corner depth first search" (CDFS) algorithm. 

Here I brainstorm comparison's between the two algorithms: 
- Implementation complexity : GBFS has significantly simpler algorithmic complexity than CDFS
- Memory complexity : GBFS's has O(n) memory complexity where n is the number of elements (the list of traversed elements). CDFS has O(1) memory complexity (requires small heap allocated buffers of constant size). Note that this does not include the memory of storing the elements, only processing them. Furthermore, the GBFS algorithm could be modified to, instead of checking a separate list of elements, could be modified (with adequate data structures) to check the global vertex indexing (specifically the element field of the vertex identities).
- Time complexity : GBFS has O(n^2) time complexity though can be reduced to (approximately) O(n) if a hash set is used for the list of traversed elements). CDFS has at absolute best super-linear time complexity, though is likely in the realm of O(n log n) or O(n^2) due to the need to check element indexes (where T8code must internally search for a given element index).
- Parallelism : GBFS is not (trivially) parallelisable as it requires a single consistent global search. CDFS is easily parallelisable on a per-tree basis as elements are iterated on a per-tree basis and the per corner depth first algorithm requires no knowledge of the status of elements across tree boundaries, only the tree index of said elements.
- Vertex to Global Vertex Index Search : A convenient property of CDFS is that given some corner of some element we can determine the element to which the vertex is indexed to (vertices are identified by an element and a corner said element) by performing a depth first search of the elements around said corner and looking for the element with the smallest element index and smallest tree index. We can guarantee that the element with the smallest element index and tree index touching a given corner is the element to which the corner is indexed. With GBFS a similar result can be achieved by performing a depth first search algorithm around the vertex and repeatedly searching the global vertex index for the desired combination of the element and the corner. This property for reordering element corners to achieve mesh conformity.

## Algorithm Comparison Summary
- The implementation complexity of GBFS is significantly simpler than CDFS. This is important for maintainability and debugging.
- The memory complexity of CDFS is O(1) compared to O(n) for GBFS. Note that GBFS could be modified to have no additional memory allocations at the cost of a non-reducible O(n^2) algorithmic complexity. Recalling previous advice from Dr. Calo I believe this is an important consideration.
- Both algorithms have comparable super-linear time complexity (though GBFS's could be reduced at the cost of memory).
- CDFS is trivially parallelisable while GBFS is not (to my knowledge) paralellisable. This is important for modern hardware and especially for future extensibility, particularly in high-performance computing environments.
- Both algorithms have the ability to trace a corner of element to it's global vertex index by performing a DFS search about the corner. Both algorithms have a worst-case time complexity of O(n) though CDFS likely has a time complexity of O(log n). Considering implementation it is my opinion that CDFS is preferable in this regard.

# Algorithm Discussion Results
While discussing the above via email with Dr. Martin and Dr, Calo, Dr. Calo provided the following algorithm (using ChatGPT and Claude) 
```julia
for tree in forest  
   for element in tree  
       for face in faces(element)  
  
           neigh = face_neighbor(element, face)  
  
           if neigh !== nothing  
  
               mapping = corner_mapping(  
                   element,  
                   neigh,  
                   face  
               )  
  
               for (c1,c2) in mapping  
                   union!(  
                       dsu,  
                       vertex_id(element,c1),  
                       vertex_id(neigh,c2)  
                   )  
               end  
           end  
       end  
   end  
end  
```
This algorithm uses the disjoint-set-union (DSU) data structure to represent the equivalence of a corner of multiple elements as a single vertex. I will refer to this as the vertex disjoint-set-union (VDSU) algorithm. 

VDSU first begins by iterating across all elements of a mesh and all local corners of said elements. The algorithm then constructs a DSU instance that represents tht e equivalence of multiple of these element local corners. Each vertex is then identified using the element with the minimum global element index that touch said vertex and the element-local corner number that corresponds to said vertex.

Note that the decision was made to instead use a global element index to identify elements as opposed to an index that relies on a tree index and a tree-local element array index to reduce the reliance on a forest of trees structured-ness.

While clarifying intent the following quote was confirmed by Dr. Martin to be a correct understanding of the current task:
> [!quote]
> My goal is to generate a global indexing of the vertices of a T8code mesh. I'd like to use the disjoint-set-union algorithm provided by Dr. Calo as iterating through the element array as opposed to traversing the mesh will make handling hanging nodes, to my current knowledge, easier. Additionally, I believe it will make reordering element vertices easier by already storing sets of equivalent vertices (as well as ultimately reconstructing a mesh).
>
> I will use a global (mesh-wide) element indexing to identify elements by adding the tree element index offset to the tree-local element array index. I will identify vertices with the minimum global element index that touches said vertex and the corner number of that vertex with respect to the element.
>
> I should not focus excessively on optimising the method of obtaining a global vertex indexing at the current stage so long as I have the groundwork to continue onto the next stage of reconstructing a conforming mesh.