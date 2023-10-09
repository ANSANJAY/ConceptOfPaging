# Page Table


- **Page Table Fundamentals**
    - The page table is a critical data structure maintained by an operating system (OS) for every running process.
    - Every individual process has its `own isolated page table`.
    - Its function is to `map virtual addresses of a process's virtual address space to physical addresses in RAM`.
  
- **Virtual vs. Physical Memory**
    - Virtual memory is organized into virtual pages, and physical memory (RAM) is organized into frames.

    - `Virtual memory is considered contiguous` while `physical memory is non-contiguous`.


- **Page Table Structure and Functionality**

    - The page table `facilitates a mapping` (or linkage) between a `process's virtual memory and physical memory`.

    - It typically consists of three main columns: 
    
        - `virtual page number`
        -  `corresponding physical page number`
        -  and the` frame number`.

    - Virtual page number usually equals physical page number under normal circumstances, although exceptions exist in advanced concepts like shared memory and forking.
    - `Frame number`
        - indicates in `which frame of the physical memory` the corresponding `physical page is loaded`.

    - The `number of rows` in a page table is 
      - equal to the number of pages in a process’s virtual address space.
    
- **Address Mapping with Page Table**
    - Virtual address to physical address mapping is executed through the `page table`.
    - By using a `virtual page number as a key`, the physical page and its location in physical memory (frame number) can be determined.
    
 # Curiosity
1. **Q1: Why is it crucial for every process to have its own page table?**
   - **A1:** Each process has its own private virtual address space, which must be mapped to physical memory. A separate page table for each process ensures isolation and protection of memory spaces among different processes by preventing one process from accessing or modifying the memory contents of another process.

2. **Q2: Explain how the page table manages the mapping of virtual addresses to physical addresses in a scenario where virtual memory is fragmented into different virtual pages?**
   - **A2:** In scenarios where virtual memory is fragmented into different virtual pages, the page table keeps track of each virtual page and maps it to a corresponding physical page in RAM. Each entry in the page table contains the virtual page number, its corresponding physical page number, and the frame number where the physical page is stored in physical memory, ensuring accurate address translation and memory management.

3. **Q3: How does the OS handle situations where the physical page is not located in RAM but on the disk, and how does this impact the page table entries?**
   - **A3:** When a physical page is located on the disk instead of RAM, the corresponding entry in the page table will not have a valid frame number. The OS uses a mechanism known as "paging" or "swapping" to handle these scenarios. When a process tries to access a page that is not in RAM, a page fault occurs. The OS selects a page in RAM to be swapped out to disk, loads the needed page into RAM, and updates the page table entries accordingly to reflect the new frame number.

4. **Q4: What is the significance of having virtual memory categorized as contiguous, and physical memory as non-contiguous?**
   - **A4:** Virtual memory being contiguous means that the virtual pages are strictly laid out in ascending order, ensuring a consistent and straightforward manner of allocating and addressing memory. On the other hand, having physical memory as non-contiguous allows for flexibility, as it allows physical pages to be stored in any frame of the physical memory, thereby maximizing the utilization of available physical memory by allowing it to store pages from different processes or even different parts of the same process without requiring continuous memory blocks.

5. **Q5: Can virtual page numbers differ from physical page numbers, and in which scenarios might this occur?**
   - **A5:** Yes, in certain scenarios, virtual page numbers can differ from physical page numbers, such as in shared memory and forking processes. In shared memory, multiple processes can access the same physical memory space, but this shared physical space might be mapped to different virtual addresses in the distinct processes' virtual address spaces. During forking, although child processes might share physical pages with the parent, the virtual addresses may differ to provide isolation among them.

6. **Q6: How does the operating system decide which page to swap out to disk during a page fault?**
   - **A6:** The operating system employs page replacement algorithms, such as Least Recently Used (LRU), First-In-First-Out (FIFO), or Clock, to determine which page to swap out to the disk during a page fault. These algorithms aim to select a page that is least likely to be used in the near future, thereby minimizing the impact on the performance of the process and optimizing the use of available RAM.

# Concepts in Simple Words
- **Page Table**: It’s like a translator that helps the computer find where information is stored in physical memory (RAM) based on where the computer thinks it is in its own virtual memory. Each program running on your computer has its own private table that helps it find its stuff in the physical memory, without bumping into or interfering with other programs' stuff.

- **Virtual and Physical Memory**: Imagine you have a bookshelf (physical memory) and you have an idea of where each type of book should go (virtual memory). Even though in your mind the books are perfectly organized by type and author, in reality, they might be placed wherever there’s free space on the bookshelf. Your organization chart (page table) helps you find where each book (piece of data) is actually placed on the shelf.

- **Address Mapping**: Just like finding a friend's house using their address, the computer uses the page table to find data. It looks at the address where it thinks the data is (virtual address), checks the page table to find out where it really is (physical address), and then goes to that spot in RAM to get the data. If the data isn’t in RAM but is on the hard drive (disk) instead, the computer has to move it to RAM, updating the page table to reflect the new real address.

let's consider a simplified  representation of a page table, keeping in mind the basic structure and principles detailed in the provided transcript.

 Normally, a page table consists of at least two main columns: 
  - the virtual page number and 
  - the frame number where the corresponding physical page is stored in memory. 
  
  In some instances, as per the transcript, physical page number is also included
  
```sql
+-----------------+------------------+--------------+
| Virtual Page No | Physical Page No | Frame Number |
+-----------------+------------------+--------------+
|       0         |        0         |      3       |
+-----------------+------------------+--------------+
|       1         |        1         |      5       |
+-----------------+------------------+--------------+
|       2         |        2         |      1       |
+-----------------+------------------+--------------+
|       3         |        3         |      2       |
+-----------------+------------------+--------------+
|       4         |        4         |    Disk      |
+-----------------+------------------+--------------+
```

Explanation:
- **Virtual Page No**: This is the address as perceived by the process.
- **Physical Page No**: This represents the actual page number in the physical memory, often equal to the virtual page number under normal circumstances.
- **Frame Number**: Indicates the frame in physical memory where the actual data is stored. If the data is not stored in physical memory but rather on the disk (due to, for example, a page swap), this might be indicated differently, like with "Disk" in the example above.

Note that in practical systems, the representation and data stored in a page table can be far more complex and might contain additional details like access bits, dirty bits, etc., which are not shown in this simplified representation.