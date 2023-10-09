# Resolve External Fragmentation 📘

- **Paging and External Fragmentation**: This elucidates how paging aids in mitigating the issue of external fragmentation in memory management.
    - The intentional equivalency between `frame size in physical memory and the size of a physical page`, especially elucidated through an example on a 32-bit system where both are chosen to be four kilobytes. 

- **Physical Page and Frame Size Correlation**: This emphasizes the calculated decision to make the size of a physical page identical to the size of a frame in physical memory.
-  The justification is rooted in ensuring that a `physical page is always loaded at the boundary of a frame`, thereby preventing any wasted or unusable memory space within a frame, which would be indicative of external fragmentation.



### Curiosity 🤔

1. **Question**: What is the significance of choosing the frame size equal to the size of a physical page in memory management?
   - **Answer**: Ensuring that the frame size is equal to the physical page size is pivotal in averting external fragmentation, which occurs when there is a misalignment in the sizes, leading to unusable memory spaces and inefficiency in memory utilization.

2. **Question**: How does external fragmentation impact the performance and efficiency of a system?
   - **Answer**: External fragmentation results in wasted memory, as the memory that is fragmented (broken into non-contiguous, unusable pieces) cannot be used effectively. It can cause the system to misjudge available memory, potentially hindering performance by not optimally allocating memory to processes, and might even force the system into unnecessary paging, thereby degrading overall system performance.

3. **Question**: Can external fragmentation occur in systems that implement paging with equal frame and page sizes? If not, why?
   - **Answer**: No, external fragmentation does not occur in systems that implement paging with equal frame and page sizes. This is because, by maintaining an equal size, every page perfectly fits into a frame without leaving any unusable memory space, thereby eliminating the possibility of external fragmentation.

4. **Question**: What could be the potential issues if a system allows the physical page size to be different than the frame size in physical memory?
   - **Answer**: If the physical page size is allowed to be different from the frame size, it can result in external fragmentation, where some parts of the memory remain unused and cannot be allocated to any other process. This fragmentation not only wastes memory resources but also can impede the performance of the system due to inefficient memory utilization.

5. **Question**: In a 32-bit system, why is the frame size and physical page size often chosen as four kilobytes? Are there specific advantages to this sizing?
   - **Answer**: Four kilobytes is a commonly used page size in 32-bit systems due to a balance of minimizing page table size and reducing the number of page faults. This size is generally a good compromise, offering a balance between internal and external fragmentation and the overhead of managing more pages versus larger pages. However, the optimal page size can depend on the specific workload and system architecture.

### Concepts in Simple Words 🌟

**Understanding External Fragmentation with Paging**:
Imagine you have a bookshelf (physical memory) where you want to place books (physical pages of a process). Each shelf (frame) is designed to hold a book of a specific thickness (page size). If you place a thinner book (smaller page size) on the shelf, you might waste some space because the book doesn't fully occupy the shelf space (external fragmentation). The concept of paging ensures that the book (page) perfectly fits the shelf (frame) by making them of equal thickness (size), so no space is wasted on the shelf, preventing any gaps (external fragmentation) and making memory use efficient.


# Resolving external fragmentation through paging by ensuring the size of a physical page is equal to the frame size.

### Scenario 1: Frame Size NOT Equal to Physical Page Size (External Fragmentation)

```
+-------------------+      +------------+
|      Frame        |      | Physical   |
|                   |      | Page       |
| +------------+    |      +------------+
| | Physical   |    |
| | Page       |    |
| +------------+    |
| |   Wasted   |    |
| |   Space    |    |
| +------------+    |
+-------------------+
```

In this scenario, the physical page does not fully occupy the frame, leading to wasted space within the frame, causing external fragmentation.

### Scenario 2: Frame Size Equal to Physical Page Size (No External Fragmentation)

```
+-------------------+      +-------------------+
|      Frame        |      | Physical Page     |
|                   |      |                   |
| +-------------------+    |                   |
| | Physical Page     |    |                   |
| |                   |    |                   |
| |                   |    |                   |
| +-------------------+    |                   |
+-------------------+      +-------------------+
```

In this scenario, the physical page perfectly fits the frame, leaving no wasted space, and thus, preventing external fragmentation. This showcases the importance of ensuring the physical page size is equal to the frame size in memory management systems.


- The "Frame" box represents a frame in physical memory.
- The "Physical Page" box represents a physical page of a process.
- "Wasted Space" indicates the part of the memory frame that remains unutilized when the physical page is smaller than the frame size.

In the simpler scenario, ensuring the physical page is the same size as the frame eliminates wasted space, ensuring efficient utilization of memory, and preventing external fragmentation.


