# rust-iter-cheatsheet
Formal description of Rust `std:iter` and `itertools`

## Generator

|Lib|Function|Input|Output|
|-|-|-|-|
|`std::iter`|[`empty`](https://doc.rust-lang.org/std/iter/fn.empty.html)||$\\{\\}$|
|`std::iter`|[`from_fn`](https://doc.rust-lang.org/std/iter/fn.from_fn.html)|$f: ()\rightarrow T$|$\\{f(), f(), ..\\}: \\{T\\}$|
|`std::iter`|[`once`](https://doc.rust-lang.org/std/iter/fn.once.html)|$a: T$|$\\{a\\}: \\{T\\}$|
|`std::iter`|[`once_with`](https://doc.rust-lang.org/std/iter/fn.once_with.html)|$f: ()\rightarrow T$|$\\{f()\\}: \\{T\\}$|
|`std::iter`|[`repeat`](https://doc.rust-lang.org/std/iter/fn.repeat.html)|$a: T$|$\\{a, a, ..\\}: \\{T\\}$|
|`std::iter`|[`repeat_with`](https://doc.rust-lang.org/std/iter/fn.repeat_with.html)|$f: ()\rightarrow T$|$\\{f(), f(), ..\\}: \\{T\\}$|
|`std::iter`|[`successors`](https://doc.rust-lang.org/std/iter/fn.successors.html)|$a: T, f: ()\rightarrow T$|$\\{a, f(), f(), ..\\}: \\{T\\}$|
|`std::iter`|[`zip`](https://doc.rust-lang.org/std/iter/fn.zip.html)|$\\{a_0, a_1, .., a_{n-1}\\}: \\{T\\}$, $\\{b_0, b_1, .., b_{m-1}\\}: \\{U\\}$|$\\{(a_0, b_0), (a_1, b_1), .., (a_i, b_i)\\}: \\{(T, U)\\} \text{wh. } i = min(n-1, m-1)$|
|`itertools`|[`chain`](https://docs.rs/itertools/latest/itertools/fn.chain.html)|$\\{a_0, a_1, .., a_{n-1}\\}: \\{T\\}$, $\\{b_0, b_1, .., b_{m-1}\\}: \\{T\\}$|$\\{a_0, a_1, .., a_{n-1}, b_0, b_1, .., b_{m-1}\\}: \\{T\\}$|
|`itertools`|[`concat`](https://docs.rs/itertools/latest/itertools/fn.concat.html)|$\\{\\{a^0_0, a^0_1, .., a^0_{n_0-1}\\}, \\{a^1_0, a^1_1, .., a^1_{n_1-1}\\}, .., \\{a^m_0, a^m_1, .., a^m_{n_m-1}\\}\\}: \\{\\{T\\}\\}$|$\\{a^0_0, a^0_1, .., a^0_{n_0-1}, a^1_0, a^1_1, .., a^1_{n_1-1}, .., a^m_0, a^m_1, .., a^m_{n_m-1}\\}: \\{T\\}$|
|`itertools`|[`cons_tuples`](https://docs.rs/itertools/latest/itertools/fn.cons_tuples.html)|$\\{(..(a^0_0, a^1_0), .., a^{m-1}_0), (..(a^0_1, a^1_1), .., a^{m-1}_1), .., (..(a^0_i, a^1_i), .., a^{m-1}_i)\\}: \\{(..(T^0, T^1), .., T^{m-1})\\}$|$\\{(a^0_0, a^1_0, .. a^{m-1}_0), (a^0_1, a^1_1, .. a^{m-1}_1), .., (a^0_i, a^1_i, .. a^{m-1}_i)\\}: \\{(T^0, T^1, .., T^{m-1})\\}$|
|`itertools`|[`diff_with`](https://docs.rs/itertools/latest/itertools/fn.diff_with.html)|$\\{a_0, a_1, .., a_{n-1}\\}: \\{T\\}$, $\\{b_0, b_1, .., b_{m-1}\\}: \\{T\\}$, $p: (T, T)\rightarrow bool$|$\textbf{Shorter}(\\{a_m, a_{m+1}, .., a_{n-1}\\})$ if $n>m\wedge p(a_0, b_0)\wedge p(a_1, b_1)\wedge ..\wedge p(a_{m-1}, b_{m-1})$, $\textbf{Longer}(\\{b_n, b{n+1}, .., b_{m-1}\\})$ if $n\lt m\wedge p(a_0, b_0)\wedge p(a_1, b_1)\wedge ..\wedge p(a_{n-1}, b_{n-1})$, $\textbf{FisrtMismatch}(i, \\{a_i, a_{i+1}, .., a_{n-1}\\}, \\{b_i, b_{i+1}, .., b_{m-1}\\})$ if $p(a_0, b_0)\wedge p(a_1, b_1)\wedge ..\wedge p(a_{i-1}, b_{i-1}) \wedge \neg p(a_i, b_i)$|
