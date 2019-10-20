# CPP Con 2019 Trip Report  (Overview)

CppCon has just ended(Edit: it's been ~ month since :) ). As I sit cramped in this tiny airplane seat, I try to process it all (yes! pretend like you wrote this on the plane ;)). While a lot of the things made sense during the talks, my notes look like a jumble of loosely connected keywords. Let's try to do reverse debugging here ...

**Venue:** Gaylord Rockies Resort, Denver, Co. It was a massive and pretty impressive hotel in middle of no where.

### Broad Topics

1. Back to Basics (new track)
2. Concurrency
3. GPU/Graphics
4. Compilers/Tooling
5. Data Structures/Allocation
6. Design/Best Practices
7. Future of C++
8. Security/Safety

## Most Interesting Talks

### [The Best Parts of C++ - Jason Turner](https://www.youtube.com/watch?v=iz5Qx18H6lg&t=554s)

This was introduction to Back to Basics track. 

This is a fun one which discusses evolution and advantages of major C++ features. 

Best parts of C++:

0. C++ standard (since C++98)

1. `const` (helps simplify variable declarations and write clean code. Forces user to initialize values)

2. RAII (since C++98, e.g. ctors/dtors pair with scoped values ) 

3. Templates (Do not repeat yourself, Turing complete and do not need *type-erasure*)

4. `vector` containers (takes care of *copy elison*)

5. Algo & STL (e.g. `for_each`, `any_of`)

6. `std::array` (fixed size at compile time -> more crazy optimization)

7. List initialization (c++11)

8. Variadic Templates (critical for implementing std::function)

9. `constexpr` (since c++11, reduced restrictions in c++20)

10. `auto` (since C++11, )

11. `auto` Return type deduction (since c++14, allows for creation of generic  `lambda`s)

12. Lambda (since c++11)

13. Generic and variadic lambda (since c++14)

14. range based for loop (since c++11, `for (const auto))

15. structured bindings (c++17, `const auto &[e1, e2] = something`)

16. Concepts (C++20, simplifies writing templated /`SFINAE`  code , can defined easily from type traits)

17. `string_view` (C++17, cheaper than copying strings from const char*)

18. Text Formatting (some nice features  e.g. positional,named args (python like) coming C++20,)

19. ranges (allows piping operations, C++ 20)

20. CTAG (class template argument deduction, gian impact for arrays C++17)

21. Rvalue references (C++11)

22. Guaranteed Copy Elision (C++17, compilers have done it historically)

23. Defaulted and Deleted functions (C++ 11)

24. `std::unique_ptr `(c++11) (safety by default)

25. fold expressions (for variadic expansions, C++17)

    

### [Speed is found in the minds of people - Andrei Alexandrescu](https://www.youtube.com/watch?v=FJJTYQYB1JQ)

This was extremely entertaining and insightful. It shows why creativity is important part when optimizing software. Andrei Alexandrescu talks about his experiments with optimizing sorting for small datasets. 

**Key Takeaways:**

1. First level thinking: 
   1. Try Silly things - Andrei's sorting algorithm does more work (create a heap before doing insertion sort) and special tricks for last element , but still is better than standard algorithms for small data sets.
   2.  Question the metrics used for designing the algorithm. [Parametric complexity theory]( https://en.wikipedia.org/wiki/Parameterized_complexity )
2. Second level thinking: Generic Programming can prevent from achieving performance. Related paper [P1393:  A General Property Customization Mechanism]( http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2019/p1393r0.html )



### [Asynchronous Programming in Modern C++ - Hartmut Kaiser](https://www.youtube.com/watch?v=_qzMpk-22cc)

Hartmut Kaiser talks about [HPX]( https://github.com/STEllAR-GROUP/hpx)

<img src="C:\Users\shelleyg\AppData\Roaming\Typora\typora-user-images\1572375636568.png" style="zoom:30%;">



### SG14 Meeting

Researches from Sandia National Labs presented their paper  [A free function Linerar algebra interface based on the BLAS](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2019/p1673r0.md) for C++23.

**Interesting highlights**

- This paper takes advantage of [`mdspan` paper](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2019/p0009r9.html) which defines types and functions for mapping multidimensional indices and [`mdarray`](https://isocpp.org/files/papers/P1684R0.pdf)
- There is some talk about optionally providing "batched" gemm interfaces. Batched gemm standardization effort  http://icl.utk.edu/bblas/ 
- Mixed precision computation supported.
- "Like the C++ Standard Library's algorithms, our operations take an
    optional execution policy argument.  This is a hook to support
    parallel execution and hierarchical parallelism (through the
    proposed executor extensions to execution policies, see
    [  Integrating Executors with Parallel Algorithms - P1019R2](http://wg21.link/p1019r2))"



### [C++ ABI from ground up - Louise Dionne](https://www.youtube.com/watch?v=DZ93lP1I7wU)

Louise Dionne who is developer of Apple's std library gives an interesting overview of how ABI compatibility can break. He gives example of Unix + Itanium C++ ABI , but the issues are universal.  ABI stability is important for

- distributing binary without source
- plug and play binaries in your code without rebuilding. 



### [RAII and Rule of Zero - Arthur O'Dwyer](https://www.youtube.com/watch?v=7Qgd9B1KuMQ)

This  is a really useful introduction to resource management. Arthur O'  Dwyer is amazing at explaining 

advanced concepts. 

**Key Takeaways:**

1. RAII (Resource Acquistion is Initialization) is really about resource cleanup.
2. <img src="C:\Users\shelleyg\AppData\Roaming\Typora\typora-user-images\1572281581515.png" style="zoom:30%;">



**Related Talks**

[RVO - Arthur O'Dwyer]( https://www.youtube.com/watch?v=hA1WNtNyNbo)

[Initialization in Modern C++]( https://www.youtube.com/watch?v=ZfP4VAK21zc )



### [From Algorithm to Generic Parallel Code : Diemeter Kuhl](https://www.youtube.com/watch?v=RrG_A7Ybzo4)

Dimeter Kuhl talks about his purely curiosty driven  study on parallelizing inclusive scan using OpenMP and TBB.  *Inclusive scan*: this seemingly simple (sequentially O(n)) operation is tricky to parallelize since each result depends on the previous.

<img src="C:\Users\shelleyg\AppData\Roaming\Typora\typora-user-images\1572137974769.png" style="zoom:30%;">



Parallel algorithm of inclusive scan divides the data into chunks and partial sums of these chunks are computed in parallel. Performance is compared between standard algorithms, OpenMP and TBB on an Intel Xeon Phi.



## Other Talks

### [C++20: C++ at 40 : Bjarne Stroustrup](https://www.youtube.com/watch?v=u_ij0YNkFUs)

"If you do it right, nobody can see it", Bjarane Stroustrup.

Bjarne Stroustrup in his supremely humble way talks about design principles of C++. 

<img src="C:\Users\shelleyg\AppData\Roaming\Typora\typora-user-images\1572135215907.png" style="zoom:60%;">



### Move Sematics: Klaus Iglberger ([Part 1]( https://www.youtube.com/watch?v=pIzaZbKUw2s) & [2](https://www.youtube.com/watch?v=pIzaZbKUw2s))

Klaus Iglberger gives an in-depth and engaging introduction to l-values, r-values, `std::move` and `srd::forward`. The most fun part were the quizzes for the audience in between each concept which clarified subtle points. 

<img src="C:\Users\shelleyg\AppData\Roaming\Typora\typora-user-images\1572136292211.png" alt="1572136292211" style="zoom:30%;" />

**Key Takeaways:**

1. Prefer simple ways of passing information

<img src="C:\Users\shelleyg\AppData\Roaming\Typora\typora-user-images\1572136613185.png" style="zoom:100%;">

2. **Rule of zero**: (Core guideline C2.0) If you can avoid defining default operations, do.

3. [TODO]Return Value optimization and antipatterns



### [Behind Enemy Lines - Reverse Engineering C++ in Modern Ages - Gal Zaban](https://www.youtube.com/watch?v=ZJpvdl_VpSM)

Gal Zaban hacks a game called "chicken invader" by reverse debugging through assembly of the game. This is a fun talk which shows the power of reverse debugging. [IDA]( https://www.hex-rays.com/products/ida/ ) Pro is used for disassembling and debugging.

### [Compiled C++ Coding Standards - Valentin Galea](https://www.youtube.com/watch?v=j0CYkFPGjNg&t=3s)

Valentin Galea presents how his team made their coding standard  super convenient to use by making it compilable. It also prevents the standard from decaying over time and makes it democratic since changes in the standard are go through code review.



### [There are No Zero-cost Abstractions: Chandler Carruth](https://www.youtube.com/watch?v=rHIkrotSwcc)

Chandler Caruth makes a case for why generic programming is not always free, through some examples in Google's code base which suffer from high compiling, linking time (e.g. protocol buffers while highly useful for representing complex data structure, moving them can be really expensive)

**Key Takeaways**

1. Moving abstractions from runtime to build time doesn't make them free.
2. unique ptr may not have the same runtime cost as raw pointer.



### [Type Punning in Modern C++: Timour Doumler](https://www.youtube.com/watch?v=_qzMpk-22cc)

Timour Doumler talks about dangers of doing type punning using c-style casts, unions etc. 

Type punning is undefined behaviour because of

- Aliasing Rules
- Lifetime of an object
- Alignment rulees
- Rules for value representation. (Related paper : [Signed Ints are Two's Complement](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2018/p0907r4.html ))

**Key Takeaways:**

1. Don't use C style casts.
2. Don't use union for type punning.
3. Use std::memcpy(std::variant)
4. [Implicity Creation of Objects for low-level object manipulation](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2019/p0593r4.html)

### [Small is beautiful: Tenchniques to minimise memory footprint - Steven Pigeon](https://www.youtube.com/watch?v=Dxy66x6v4HE)

Steven Pigeon who is professor at UQAR talks about his really interesting work on compressed pointers. 

### [The amazing story of implementing Concepts in Clang - Saar Raz](https://www.youtube.com/watch?v=Y1o4rc9P1FQ)

Saar Raz talks about his super interesting story of how he implemented Concepts in Clang without any previous knowledge of the clang='s code base.  

### [Smart Poiners - Arthur O'Dwyer](https://www.youtube.com/watch?v=xGDLkt-jBJ4)

Arthur O'Dwyer gives a really good introduction into why and how of smart of pointers.

### [Better Code: Relationships - Sean Parent](https://www.youtube.com/watch?v=ejF6qqohp3M)

Sean parent talks about art of designing relationships in your code. One particular example he gives is one has to think about safety and efficiency when managing resources and often one is compromised in favor of another (e.g. `std::move` is unsafe operation)

### [De-fragmenting C++ - Herb Sutter](https://www.youtube.com/watch?v=ARYP83yNAWk)

This is the closing keynote.  Herb Sutter talks about his future proposals for  C++,  on how to reduce cost of RTII and exceptions while also abstracting complexity.



### [What is C++ - Chandler Carruth, Titus Winters](https://www.youtube.com/watch?v=LJh5QCV4wDg)

This is the closing keynote of the back to basics track, which is wonderful discussion on design and pitfalls of C++ standard. 









