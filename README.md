
# OS Page Replacement Visualizer

This repository contains an **Operating System Page Replacement Algorithm Visualizer**, designed to help understand how different page replacement policies work.

🔗 **[OS Page Replacement Visualizer](https://amritlathar.github.io/OS-PageReplacement/presentation.html)**

---

## 📌 Algorithms Implemented

Below are the algorithms available in the visualizer with a short explanation and a worked example.

---

### 1. FIFO (First In First Out)
- **Idea**: Replace the oldest loaded page (first inserted).
- **Pros**: Easy to implement.
- **Cons**: Can suffer from Belady's anomaly.

**Example**:  
Pages: `7, 0, 1, 2, 0, 3, 0, 4` | Frames: `3`

| Step | Page | Frames (Oldest → Newest) | Fault? |
|------|------|--------------------------|--------|
| 1    | 7    | 7                        | ✅     |
| 2    | 0    | 7 0                      | ✅     |
| 3    | 1    | 7 0 1                    | ✅     |
| 4    | 2    | 0 1 2                    | ✅     |
| 5    | 0    | 0 1 2                    | ❌     |
| 6    | 3    | 1 2 3                    | ✅     |
| 7    | 0    | 2 3 0                    | ✅     |
| 8    | 4    | 3 0 4                    | ✅     |

---

### 2. LRU (Least Recently Used)
- **Idea**: Replace the page that has not been used for the longest time.
- **Pros**: Often better than FIFO.
- **Cons**: Requires tracking page usage history.

| Step | Page | Frames (LRU → MRU) | Fault? |
|------|------|--------------------|--------|
| 1    | 7    | 7                  | ✅     |
| 2    | 0    | 7 0                | ✅     |
| 3    | 1    | 7 0 1              | ✅     |
| 4    | 2    | 0 1 2              | ✅     |
| 5    | 0    | 1 2 0              | ❌     |
| 6    | 3    | 2 0 3              | ✅     |
| 7    | 0    | 0 3 2              | ❌     |
| 8    | 4    | 3 2 4              | ✅     |

---

### 3. LFU (Least Frequently Used)
- **Idea**: Replace the page used least often so far.
- **Pros**: Keeps frequently used pages longer.
- **Cons**: Can evict a recently used page with low frequency.

| Step | Page | Frames | Frequency Count | Fault? |
|------|------|--------|-----------------|--------|
| 1    | 7    | 7      | 7(1)            | ✅     |
| 2    | 0    | 7 0    | 7(1) 0(1)       | ✅     |
| 3    | 1    | 7 0 1  | 7(1) 0(1) 1(1)  | ✅     |
| 4    | 2    | 0 1 2  | 0(1) 1(1) 2(1)  | ✅     |
| 5    | 0    | 0 1 2  | 0(2) 1(1) 2(1)  | ❌     |
| 6    | 3    | 1 2 3  | 1(1) 2(1) 3(1)  | ✅     |
| 7    | 0    | 0 2 3  | 0(3) 2(1) 3(1)  | ✅     |
| 8    | 4    | 0 4 3  | 0(3) 4(1) 3(1)  | ✅     |

---

### 4. MFU (Most Frequently Used)
- **Idea**: Replace the page with the highest usage count.
- **Pros**: Assumes frequently used pages might be done soon.
- **Cons**: Usually worse than LFU.

| Step | Page | Frames | Frequency Count | Fault? |
|------|------|--------|-----------------|--------|
| 1    | 7    | 7      | 7(1)            | ✅     |
| 2    | 0    | 7 0    | 7(1) 0(1)       | ✅     |
| 3    | 1    | 7 0 1  | 7(1) 0(1) 1(1)  | ✅     |
| 4    | 2    | 2 0 1  | 2(1) 0(1) 1(1)  | ✅     |
| 5    | 0    | 0 2 1  | 0(2) 2(1) 1(1)  | ❌     |
| 6    | 3    | 3 2 1  | 3(1) 2(1) 1(1)  | ✅     |
| 7    | 0    | 0 2 3  | 0(3) 2(1) 3(1)  | ✅     |
| 8    | 4    | 4 2 3  | 4(1) 2(1) 3(1)  | ✅     |

---

### 5. Optimal (OPT)
- **Idea**: Replace the page that will not be used for the longest time in the future.
- **Pros**: Gives the lowest possible page faults.
- **Cons**: Requires future knowledge (ideal for comparison only).

| Step | Page | Frames | Fault? | Reason |
|------|------|--------|--------|--------|
| 1    | 7    | 7      | ✅     | Empty frame |
| 2    | 0    | 7 0    | ✅     | Empty frame |
| 3    | 1    | 7 0 1  | ✅     | Empty frame |
| 4    | 2    | 2 0 1  | ✅     | 7 used farthest in future |
| 5    | 0    | 2 0 1  | ❌     | 0 already in frame |
| 6    | 3    | 3 0 1  | ✅     | 2 used farthest in future |
| 7    | 0    | 3 0 1  | ❌     | 0 in frame |
| 8    | 4    | 4 0 1  | ✅     | 3 used farthest in future |

---

### 6. Random
- **Idea**: Pick any page at random to replace.
- **Pros**: Very simple.
- **Cons**: Performance unpredictable.

**Example** (random choices shown):  
| Step | Page | Frames | Fault? |
|------|------|--------|--------|
| 1    | 7    | 7      | ✅     |
| 2    | 0    | 7 0    | ✅     |
| 3    | 1    | 7 0 1  | ✅     |
| 4    | 2    | 2 0 1  | ✅     |
| 5    | 0    | 2 0 1  | ❌     |
| 6    | 3    | 3 0 1  | ✅     |
| 7    | 0    | 3 0 1  | ❌     |
| 8    | 4    | 4 0 1  | ✅     |

---

### 7. Second Chance (Clock)
- **Idea**: FIFO with a reference bit. If bit=1, give a “second chance” and move it to the back.
- **Pros**: Avoids replacing frequently used pages.
- **Cons**: Slightly more complex than FIFO.

| Step | Page | Frames (Clock order) | Ref Bits | Fault? |
|------|------|----------------------|----------|--------|
| 1    | 7    | 7                    | 1        | ✅     |
| 2    | 0    | 7 0                  | 1 1      | ✅     |
| 3    | 1    | 7 0 1                | 1 1 1    | ✅     |
| 4    | 2    | 2 0 1                | 1 1 1    | ✅     |
| 5    | 0    | 2 0 1                | 1 1 1    | ❌     |
| 6    | 3    | 3 0 1                | 1 1 1    | ✅     |
| 7    | 0    | 3 0 1                | 1 1 1    | ❌     |
| 8    | 4    | 4 0 1                | 1 1 1    | ✅     |

---

## 🚀 How to Use
1. Open the **[Visualizer Link](https://amritlathar.github.io/OS-PageReplacement/presentation.html)**.
2. Select an algorithm.
3. Enter page reference string and frame size.
4. Step through to watch how pages are replaced.

---

## 📂 Repository Structure
