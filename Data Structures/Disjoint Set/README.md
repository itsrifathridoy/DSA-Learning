# Disjoint Sets (Union-Find) Data Structure

This repository contains implementations and explanations of the Disjoint Set data structure (also known as Union-Find) in C++.

## Table of Contents
1. [Introduction](#introduction)
2. [Conceptual Understanding](#conceptual-understanding)
3. [Operations and Implementation](#operations-and-implementation)
4. [Data Structure Design](#data-structure-design)
5. [Visualizations and Examples](#visualizations-and-examples)
6. [Code Implementation](#code-implementation)
7. [Applications and Complexity](#applications-and-complexity)
8. [Contributing](#contributing)
9. [License](#license)

## Introduction
- Have you ever wondered how social media platforms determine friend connections among millions of users?

- Imagine a scenario where you need to efficiently group data into subsets based on specific attributes. How would you tackle this challenge?


Disjoint Sets, often implemented using the Union-Find data structure, are utilized to manage sets of elements partitioned into disjoint subsets. This repository serves as a resource to understand and implement this data structure efficiently.

## Conceptual Understanding

### Sets and Disjoint Sets

In computer science, a set is a collection of distinct elements. Disjoint Sets refer to sets in which no element is shared between any two sets, i.e., they have no elements in common.

### Disjoint Set Data Structure

The Disjoint Set (also known as Union-Find) data structure is used to manage disjoint sets and perform operations efficiently on them. It is particularly useful in scenarios where elements need to be partitioned into distinct sets and determine relationships between them.

### Components

In the context of Disjoint Sets:
- **Element:** Each individual item that can be a part of a set.
- **Set:** A collection of elements grouped together. In Disjoint Sets, sets are disjoint, meaning they have no common elements with other sets.
- **Representative Element:** Each set has one representative element used to identify the set and perform operations like union and find efficiently.

### Key Concepts
- **Connectivity:** Disjoint Sets assist in understanding the relationships or connections between elements.
- **Partitioning:** They aid in partitioning a larger set of elements into distinct subsets, facilitating various algorithms that require partitioned data.

Understanding these fundamental concepts is essential in effectively utilizing the Disjoint Set data structure for various applications and algorithmic solutions.

## Operations and Implementation

### Operations Overview

#### Make Set
- **Description:** Creating a new set with a single element.
- **Purpose:** To initialize each element as a separate set.

#### Find (Find-Set)
- **Description:** Locating the representative element of the set to which an element belongs.
- **Purpose:** To determine if two elements belong to the same set or to identify the set an element belongs to.

#### Union
- **Description:** Merging two disjoint sets into a single set.
- **Purpose:** To combine sets, establishing a relationship between previously disjoint sets.

### Implementation Details

#### Data Structure Representation
Disjoint Sets can be implemented using various data structures, such as arrays, trees, or graphs, to represent sets and perform operations efficiently.

##### Array-Based Implementation
- **Representation:** Using an array to store elements where each index corresponds to an element, and the value at each index points to the parent of the element.
- **Operations:**
  - **Make Set:** Initialize each element with itself as its parent.
  - **Find:** Traverse the parent pointers until reaching the representative element.
  - **Union:** Merge sets by updating the parent pointer of one set's representative to point to the other set's representative.

##### Optimizations
Disjoint Sets can be optimized using two common techniques:

###### Path Compression
- **Description:** During the find operation, path compression modifies the structure of the tree, flattening it by making every node point directly to the root.
- **Implementation:** Modify the parent pointers to directly link each element to its representative during find operations.

###### Union by Rank (or Union by Size)
- **Description:** This optimization maintains the balance of the tree by always attaching the smaller tree to the root of the larger tree during the union operation.
- **Implementation:** Keep track of the rank/size of each set and merge smaller sets into larger ones during union operations.

## Visualizations and Examples

### Visual Aids
Include diagrams or animations to illustrate Disjoint Set operations visually.

### Real-World Examples
Demonstrate applications where Disjoint Sets are used, such as network connectivity problems or image segmentation.

## Code Implementation

### Language: C++

#### Array-Based Implementation

##### Overview
An example implementation of Disjoint Sets using arrays as the underlying data structure.

```cpp
#include <iostream>
#include <vector>

using namespace std;

class DisjointSets {
private:
    vector<int> parent;

public:
    DisjointSets(int n) {
        parent.resize(n);
        // Initializing each element as a separate set with itself as the parent
        for (int i = 0; i < n; ++i) {
            parent[i] = i;
        }
    }

    // Find operation: Find the representative element of the set to which element x belongs
    int find(int x) {
        if (parent[x] == x) {
            return x;
        }
        return find(parent[x]); // Without Path compressio
    }

    // Union operation: Merge two sets to which elements x and y belong
    void Union(int x, int y) {
        int rootX = find(x);
        int rootY = find(y);
        if (rootX != rootY) {
            parent[rootX] = rootY;
        }
    }
};
```
## Optimizations

 - Path Compression
   
```cpp
    // Find operation with path compression
    int findWithPathCompression(int x) {
        if (parent[x] == x) {
            return x;
        }
        return parent[x] = findWithPathCompression(parent[x]); // Path compression
    }
```
   Path compression optimizes the find operation by flattening the tree structure.

 - Union by Rank (or Size)

   ```cpp
   // Additional optimization: Union by rank
    void unionByRank(int x, int y) {
        int rootX = find(x);
        int rootY = find(y);
        if (rootX != rootY) {
            if (rank[rootX] < rank[rootY]) {
                parent[rootX] = rootY;
            } else if (rank[rootX] > rank[rootY]) {
                parent[rootY] = rootX;
            } else {
                parent[rootY] = rootX;
                rank[rootX]++;
            }
        }
    }
Union by rank optimizes the union operation by attaching the smaller tree to the larger tree.

## Applications and Complexity

### Applications

#### Kruskal's Minimum Spanning Tree Algorithm
- **Description:** Disjoint Sets are used in Kruskal's algorithm to find the Minimum Spanning Tree (MST) of a connected, edge-weighted graph.
- **Implementation:** They help identify and merge the disjoint sets of vertices, ensuring that only safe edges (edges that do not form cycles) are included in the MST.

#### Connected Components in Graphs
- **Description:** Disjoint Sets efficiently identify connected components in graphs.
- **Implementation:** They determine which vertices belong to the same component and which are disconnected.

#### Image Segmentation
- **Description:** In image processing, Disjoint Sets can be used for image segmentation, dividing an image into regions based on pixel similarities.
- **Implementation:** They assist in grouping pixels together based on similarity metrics, creating distinct segments in the image.

### Time Complexity

#### Find Operation
- **Complexity:** O(log n) with path compression.
- **Explanation:** Path compression optimizes the tree height, ensuring subsequent find operations have a reduced time complexity.

#### Union Operation
- **Complexity:** O(log n) with union by rank or size.
- **Explanation:** Union by rank/size maintains balanced trees, preventing tall trees and ensuring efficient union operations.

#### Overall Complexity
- **Complexity:** Generally, the overall time complexity for a sequence of n operations is nearly linear, O(n * α(n)), where α(n) is the inverse Ackermann function, which grows extremely slowly for any practical n values.
- **Explanation:** This near-linear complexity ensures efficient performance for most practical scenarios involving Disjoint Sets.

### Space Complexity
- **Complexity:** O(n)
- **Explanation:** The space complexity primarily depends on the number of elements in the Disjoint Sets data structure, requiring space proportional to the number of elements for parent and rank arrays or other required data structures.

## Contributing

Contributions are welcome! Please follow the guidelines outlined in [CONTRIBUTING.md](link-to-contributing-guidelines).

## License

This project is licensed under the [MIT License](LICENSE.md), allowing free use, modification, and distribution under certain conditions.

