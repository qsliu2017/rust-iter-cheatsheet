# rust-iter-cheatsheet
Formal description of Rust `std:iter` and `itertools`

## Generator

|Function|Input|Output|
|-|-|-|
|[`empty`](https://doc.rust-lang.org/std/iter/fn.empty.html)||$\\{\\}$|
|[`from_fn`](https://doc.rust-lang.org/std/iter/fn.from_fn.html)|$f: ()\rightarrow T$|$\\{f(), f(), ..\\}: \\{T\\}$|
|[`once`](https://doc.rust-lang.org/std/iter/fn.once.html)|$a: T$|$\\{a\\}: \\{T\\}$|
|[`once_with`](https://doc.rust-lang.org/std/iter/fn.once_with.html)|$f: ()\rightarrow T$|$\\{f()\\}: \\{T\\}$|
|[`repeat`](https://doc.rust-lang.org/std/iter/fn.repeat.html)|$a: T$|$\\{a, a, ..\\}: \\{T\\}$|
|[`repeat_with`](https://doc.rust-lang.org/std/iter/fn.repeat_with.html)|$f: ()\rightarrow T$|$\\{f(), f(), ..\\}: \\{T\\}$|
|[`successors`](https://doc.rust-lang.org/std/iter/fn.successors.html)|$a: T, f: ()\rightarrow T$|$\\{a, f(), f(), ..\\}: \\{T\\}$|
|[`zip`](https://doc.rust-lang.org/std/iter/fn.zip.html)|$\\{a_0, a_1, .., a_{n-1}\\}: \\{T\\}$, $\\{b_0, b_1, .., b_{m-1}\\}: \\{U\\}$|$\\{(a_0, b_0), (a_1, b_1), .., (a_i, b_i)\\}: \\{(T, U)\\} \text{wh. } i = min(n-1, m-1)$|
|*[`chain`](https://docs.rs/itertools/latest/itertools/fn.chain.html)|$\\{a_0, a_1, .., a_{n-1}\\}: \\{T\\}$, $\\{b_0, b_1, .., b_{m-1}\\}: \\{T\\}$|$\\{a_0, a_1, .., a_{n-1}, b_0, b_1, .., b_{m-1}\\}: \\{T\\}$|
|*[`concat`](https://docs.rs/itertools/latest/itertools/fn.concat.html)|$\\{\\{a^0_0, a^0_1, .., a^0_{n_0-1}\\}, \\{a^1_0, a^1_1, .., a^1_{n_1-1}\\}, .., \\{a^m_0, a^m_1, .., a^m_{n_m-1}\\}\\}: \\{\\{T\\}\\}$|$\\{a^0_0, a^0_1, .., a^0_{n_0-1}, a^1_0, a^1_1, .., a^1_{n_1-1}, .., a^m_0, a^m_1, .., a^m_{n_m-1}\\}: \\{T\\}$|
|*[`cons_tuples`](https://docs.rs/itertools/latest/itertools/fn.cons_tuples.html)|$\\{(..(a^0_0, a^1_0), .., a^{m-1}_0), (..(a^0_1, a^1_1), .., a^{m-1}_1), .., (..(a^0_i, a^1_i), .., a^{m-1}_i)\\}: \\{(..(T^0, T^1), .., T^{m-1})\\}$|$\\{(a^0_0, a^1_0, .. a^{m-1}_0), (a^0_1, a^1_1, .. a^{m-1}_1), .., (a^0_i, a^1_i, .. a^{m-1}_i)\\}: \\{(T^0, T^1, .., T^{m-1})\\}$|
|*[`diff_with`](https://docs.rs/itertools/latest/itertools/fn.diff_with.html)|$\\{a_0, a_1, .., a_{n-1}\\}: \\{T\\}$, $\\{b_0, b_1, .., b_{m-1}\\}: \\{T\\}$, $p: (T, T)\rightarrow bool$|$\textbf{Shorter}(\\{a_m, a_{m+1}, .., a_{n-1}\\})$ if $n>m\wedge p(a_0, b_0)\wedge p(a_1, b_1)\wedge ..\wedge p(a_{m-1}, b_{m-1})$, $\textbf{Longer}(\\{b_n, b{n+1}, .., b_{m-1}\\})$ if $n\lt m\wedge p(a_0, b_0)\wedge p(a_1, b_1)\wedge ..\wedge p(a_{n-1}, b_{n-1})$, $\textbf{FisrtMismatch}(i, \\{a_i, a_{i+1}, .., a_{n-1}\\}, \\{b_i, b_{i+1}, .., b_{m-1}\\})$ if $p(a_0, b_0)\wedge p(a_1, b_1)\wedge ..\wedge p(a_{i-1}, b_{i-1}) \wedge \neg p(a_i, b_i)$|

- [ ] left functions in itertools, see https://docs.rs/itertools/latest/itertools/#functions

## Transform

|Method|Input|Output|
|-|-|-|
|[`advance_by`](https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.advance_by)|$a=\\{a_0, a_1, .., a_{m-1}\\}: \\{T\\}$, $n$|$\textbf{Ok}$, if $n\le m$, $\textbf{Err}(m)$ if $n\gt m$. *Side Effect*: $a\leftarrow \\{a_n, a_{n+1}, .., a_{m-1}\\}$ if $n\le m$, $a\leftarrow \\{\\}$ if $n\gt m$|
|[`chain`](https://docs.rs/itertools/latest/itertools/fn.chain.html)|$\\{a_0, a_1, .., a_{n-1}\\}: \\{T\\}$, $\\{b_0, b_1, .., b_{m-1}\\}: \\{T\\}$|$\\{a_0, a_1, .., a_{n-1}, b_0, b_1, .., b_{m-1}\\}: \\{T\\}$|
|[`cmp`](https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.cmp)|$\\{a_0, a_1, .., a_{n-1}\\}: \\{T\\}$, $\\{b_0, b_1, .., b_{m-1}\\}: \\{T\\}$|$\\{a_0.\text{cmp}(b_0), a_1.\text{cmp}(b_1), .., a_i.\text{cmp}(b_i)\\}: {\\{\textbf{Ordering}\\}}$ where $i=\text{min}(n,m)-1$|
|[`cmp_by`](https://docs.rs/itertools/latest/itertools/fn.cmp_by.html)|$\\{a_0, a_1, .., a_{n-1}\\}: \\{T\\}$, $\\{b_0, b_1, .., b_{m-1}\\}: \\{T\\}$, $f: (T, T)\rightarrow \textbf{Ordering}$|$\\{f(a_0, b_0), f(a_1, b_1), .., f(a_i, b_i)\\}: {\\{\textbf{Ordering}\\}}$ where $i=\text{min}(n,m)-1$|
|[`cycle`](https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.cycle)|$\\{a_0, a_1, .., a_{n-1}\\}$|$\\{a_0, a_1, .., a_{n-1}, a_1, a_2, ..\\}$|
|[`enumerate`](https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.enumerate)|$\\{a_0, a_1, .., a_{n-1}\\}: \\{T\\}$|$\\{(0, a_0), (1, a_1), .., (n-1, a_{n-1})\\}: \\{(\text{usize}, T)\\}$|
|[`filter`](https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.filter)|$\\{a_0, a_1, .., a_{n-1}\\}: \\{T\\}$, $p: T\rightarrow bool$|$\\{a_{i_0}, a_{i_1}, .., a_{i_{m-1}}\\}: \\{T\\}$ where $\forall k$ $p(a_{i_k})=\textbf{true}$|
|[`filter_map`](https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.filter_map)|$\\{a_0, a_1, .., a_{n-1}\\}: \\{T\\}$, $f: T\rightarrow \textbf{Option<U>}$|$\\{b_{i_0}, b_{i_1}, .., b_{i_{m-1}}\\}: \\{U\\}$ where $\forall k$ $f(a_{i_k})=\textbf{Some}(b_{i_k})$, and the others $f(a_j)=\textbf{None}$|

## Value
|Method|Input|Output|
|-|-|-|
|[`all`](https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.all)|$a=\\{a_0, a_1, .., a_{n-1}\\}$, $p: T\rightarrow bool$|$\textbf{true}$ if $\forall i$ $p(a_i)=\textbf{true}$, otherwise $\textbf{false}$. *Side Effect*: $a\leftarrow \\{a_i, a_{i+1}, .., a_{n-1}\\}$ where $i$ is first $p(a_i)=\textbf{false}$, otherwise $a\leftarrow \\{\\}$|
|[`any`](https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.any)|$a=\\{a_0, a_1, .., a_{n-1}\\}$, $p: T\rightarrow bool$|$\textbf{true}$ if $\exists i$ $p(a_i)=\textbf{true}$, otherwise $\textbf{false}$. *Side Effect*: $a\leftarrow \\{a_i, a_{i+1}, .., a_{n-1}\\}$ where $i$ is first $p(a_i)=\textbf{true}$, otherwise $a\leftarrow \\{\\}$|
|[`count`](https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.count)|$\\{a_0, a_1, .., a_{n-1}\\}$|$n$|
|[`eq`](https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.eq)|$\\{a_0, a_1, .., a_{n-1}\\}$, $\\{b_0, b_1, .., b_{m-1}\\}$|$\textbf{true}$ if $\forall i$ $a_i=b_i$, otherwise $\textbf{false}$|
|[`eq_by`](https://docs.rs/itertools/latest/itertools/fn.eq_by.html)|$\\{a_0, a_1, .., a_{n-1}\\}$, $\\{b_0, b_1, .., b_{m-1}\\}$, $f: (T, T)\rightarrow bool$|$\textbf{true}$ if $\forall i$ $f(a_i, b_i)=\textbf{true}$, otherwise $\textbf{false}$|

## Other
|Method|
|-|
|[`by_ref`](https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.by_ref)|
|[`cloned`](https://docs.rs/itertools/latest/itertools/fn.cloned.html)|
|[`collect`](https://docs.rs/itertools/latest/itertools/fn.collect.html)|
|[`collect_into`](https://docs.rs/itertools/latest/itertools/fn.collect_into.html)|
|[`copied`](https://docs.rs/itertools/latest/itertools/fn.copied.html)|


- [ ] https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.find
