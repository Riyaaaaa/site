# BOOST_PP_LIST_FOLD_LEFT_d

`BOOST_PP_LIST_FOLD_LEFT_d` マクロは *リスト* の要素を左から右へ折りたたむ（または蓄積する）。
これは `BOOST_PP_WHILE` 内で呼ばれる際には最も効率よく機能する。

## Usage

```cpp
BOOST_PP_LIST_FOLD_LEFT_ ## d(op, state, list)
```

## Arguments

- `d` :
	次の有効な `BOOST_PP_WHILE` 反復。

- `op` :
	`op (d, state, elem )` 形式の 3項演算。
	このマクロは *リスト* 中の各要素のために呼び出される―毎回新しい *状態* を返す。
	この演算は、次の有効な `BOOST_PP_WHILE` 反復、現在の *状態* および現在の要素を伴い `BOOST_PP_LIST_FOLD_LEFT` によって展開される。

- `state` :
	折りたたみの初期状態。

- `list` :
	折りたたまれる *リスト* 。

## Remarks

*リスト* `(0, (1, (2, BOOST_PP_NIL)))` のために、このマクロは

```cpp
op(d, op(d, op(d, state, 0), 1), 2)
```

に展開される。

## See Also

- [`BOOST_PP_LIST_FOLD_LEFT`](list_fold_left.md)

## Requirements

Header: &lt;boost/preprocessor/list/fold_left.hpp&gt;

## Sample Code

```cpp
#include <boost/preprocessor/cat.hpp>
#include <boost/preprocessor/list/fold_left.hpp>

#define L1 (a, (b, (c, BOOST_PP_NIL)))
#define L2 (L1, (L1, (L1, BOOST_PP_NIL)))

#define OP(d, state, x) (BOOST_PP_LIST_FOLD_LEFT_ ## d(OP_2, _, x), state)
#define OP_2(d, state, x) BOOST_PP_CAT(state, x)

BOOST_PP_LIST_FOLD_LEFT(OP, BOOST_PP_NIL, L2)
/*
	(_abc, (_abc, (_abc, BOOST_PP_NIL)))
	に展開される
*/
```
* BOOST_PP_NIL[link nil.md]
* BOOST_PP_LIST_FOLD_LEFT_[link list_fold_left_d.md]
* BOOST_PP_CAT[link cat.md]
* BOOST_PP_LIST_FOLD_LEFT[link list_fold_left.md]

