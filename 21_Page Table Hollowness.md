# Page Table Problem 3 - Page Table Hollowness

### 📘 Concepts
   - **Page Tables:**
     - Page tables are data structures used in computer operating systems to manage virtual memory, mapping virtual addresses to physical addresses.
     - In this context, each process has its page table, created as soon as the process runs on the system, even if it hasn't logged any memory.
     - The size of the page table per process is four megabytes.
   
   - **Memory Segments:**
     - Every process has mandatory segments like code segments and initialized/uninitialized data segments, each mapped to virtual pages.
     - In a simple "Hello World" program, despite consuming minimal memory, it will have some occupied virtual pages corresponding to these segments and maybe some stack memory due to the procedure call.
     - A process may only use a few virtual pages out of a possible \(2^{32} - 1\).
   
   - **Hollowness Problem:**
     - Despite only a few virtual pages being in use, the corresponding page table needs to provide entries for all possible virtual pages, leading to "hollowness" or unused entries in the table.
     - This scenario results in an inefficient memory usage, as most of the page table entries remain empty (unutilized), consuming memory but not mapping to any physical page.
     - Hollowness creates "holes" in the page table, meaning large stretches of contiguous entries are unused, lying between utilized low and high virtual pages.
     - Especially for smaller, less memory-intensive processes, this results in over 99% of the page table being wasted.
   
   - **Multi-Level Paging:**
     - Proposed as a solution to the problem of hollowness in page tables.
     - This concept will further be elaborated in subsequent discussions, explaining how it addresses the outlined problems.

### 🤔 Curiosity

   1. **Q1: How does the operating system determine the size of a page table for a process?**
      - A1: The size of a page table is typically determined based on the virtual address space of the process and the page size. For example, if a system uses paging with a virtual address space of 32 bits and a page size of 4 KB, the page table needs to have enough entries to map all possible pages that a process might use. The page table size could be determined by \([2^{(number of bits for virtual page number)}] \times size of an entry\). 

   2. **Q2: Explain how the memory is wasted in the context of hollowness in page tables?**
      - A2: Memory is wasted through the hollowness in page tables by allocating entries for all possible virtual pages, even though only a few of them might be used. Each entry in a page table, even if unused, consumes memory. When most entries (as is often the case with small processes) remain unused, this represents a substantial waste of memory, as the system reserves space for mapping that is not needed.

   3. **Q3: Why is multi-level paging considered as a solution to page table hollowness?**
      - A3: Multi-level paging is considered a solution to page table hollowness as it essentially breaks down the single, large page table into multiple smaller tables, structured hierarchically. This minimizes the memory requirement for storing page tables by only allocating memory for the tables/entries that are actually needed/used, reducing the wastage due to hollowness.

   4. **Q4: What are some potential drawbacks or challenges of implementing multi-level paging?**
      - A4: Some potential drawbacks of implementing multi-level paging might include increased complexity in the memory management code, potentially slower memory access times due to having to navigate through multiple levels of tables to resolve a physical address, and an additional overhead to manage multiple levels of page tables.

   5. **Q5: How can an OS minimize the impact on memory access times while implementing multi-level paging?**
      - A5: The OS can minimize the impact on memory access times during multi-level paging by employing techniques like caching frequently used page table entries (Translation Lookaside Buffers, or TLBs), ensuring that table lookup operations are performed quickly, or by utilizing hardware support to accelerate the lookup processes.

### 🔄 Concepts in Simple Words
   - **Page Tables:**
     - Think of a page table like a translator from one type of address (virtual) that programs use, to another type (physical) that computer memory uses.
   
   - **Memory Segments:**
     - Imagine a program being divided into sections like a book; each section (or segment) contains specific types of data or instructions, and each has a place in the memory.
   
   - **Hollowness Problem:**
     - Imagine you have a large bookshelf (page table) where only a few shelves (entries) are filled with books (data) and most are empty but still take up space. This extra, unused space is the "hollowness" in the page table.
   
   - **Multi-Level Paging:**
     - Instead of having one big bookshelf (page table), imagine having a few smaller ones (multi-level page tables), where you only add additional shelves (pages) when you get more books (data). This way, you don’t waste space with empty shelves (unused entries).
   
This breakdown should help to visualize and understand the concept of page table hollowness and provide a basis for exploring the technical aspects further.