# Solution Summary for Problem 009 - STLite Vector

## Problem Description
Implement a `vector` container similar to `std::vector` in C++ STL with:
- Dynamic array functionality with automatic memory management
- Iterator and const_iterator support
- Complete set of member functions (insert, erase, push_back, pop_back, etc.)
- Proper exception handling
- No default constructor assumption for template type T

## Implementation Approach

### Key Design Decisions

1. **Memory Management with Placement New**
   - Used `::operator new` to allocate raw memory without calling constructors
   - Used placement new `new (ptr) T(value)` to construct objects in allocated memory
   - Explicitly called destructors `~T()` before deallocation
   - This approach handles types without default constructors

2. **Dynamic Capacity Expansion**
   - Starting capacity: 0
   - Growth strategy: double the capacity when full (or start with 1 if capacity is 0)
   - Implemented in `expand_capacity()` method

3. **Iterator Implementation**
   - Both `iterator` and `const_iterator` classes implemented
   - Store pointer to element and pointer to container
   - Container pointer enables validation for operations between iterators
   - Made `vector<T>` a friend class to access private members

4. **Exception Safety**
   - Bounds checking in `at()` and `operator[]`
   - Container empty checks in `front()`, `back()`, and `pop_back()`
   - Iterator validation in subtraction operator

### Submission Results

**Submission ID:** 706670
**Final Score:** 140/140 (100%)
**Status:** Accepted

#### Test Results:
- ✅ one: Accepted (10 points)
- ✅ two: Accepted (10 points)
- ✅ three: Accepted (10 points)
- ✅ four: Accepted (10 points)
- ✅ five: Accepted (10 points)
- ✅ six: Accepted (10 points)
- ✅ seven: Accepted (10 points)
- ✅ one.memcheck: Accepted (10 points)
- ✅ two.memcheck: Accepted (10 points)
- ✅ three.memcheck: Accepted (10 points)
- ✅ four.memcheck: Accepted (10 points)
- ✅ five.memcheck: Accepted (10 points)
- ✅ six.memcheck: Accepted (10 points)
- ✅ seven.memcheck: Accepted (10 points)

**Performance Highlights:**
- Maximum memory usage: ~716 MB
- Maximum execution time: ~77 seconds (includes all tests)
- All memory checks passed (no memory leaks)

## Key Implementation Features

1. **Constructors and Destructor**
   - Default constructor initializes empty vector
   - Copy constructor uses placement new for deep copy
   - Destructor explicitly calls destructors for all elements

2. **Element Access**
   - `at()` and `operator[]` with bounds checking
   - `front()` and `back()` with empty container checks

3. **Iterators**
   - Full random access iterator interface
   - Arithmetic operators (+, -, +=, -=)
   - Comparison operators (==, !=)
   - Increment/decrement operators (++, --)

4. **Modifiers**
   - `push_back()`: Amortized O(1)
   - `pop_back()`: O(1)
   - `insert()`: O(n)
   - `erase()`: O(n)
   - `clear()`: O(n)

5. **Capacity Management**
   - `size()`: Returns current number of elements
   - `empty()`: Checks if container is empty
   - Automatic capacity expansion when needed

## Submissions Used
- **1 out of 4** submission attempts used
- **3 attempts remaining**

## Conclusion
The implementation successfully passes all test cases including memory leak checks. The solution correctly handles:
- Types without default constructors
- Dynamic memory management without leaks
- All STL vector operations
- Edge cases and exception handling
- Performance requirements within time and memory limits
