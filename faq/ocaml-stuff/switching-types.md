# Switching types

### Having a type ``a result how do I get a type `a`?``

`Several possibilities:`

* `get_ok see` [`this`](https://ocaml.org/api/Result.html#VALget\_ok) `` but it will fail if you have an `Error` ``
* `fold` see [this](https://ocaml.org/api/Result.html#VALfold) (`Result.fold ~ok:Fun.id ~error: (a_function_that_fits_error_into_a) your_result`)
* `match`
