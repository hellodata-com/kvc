KVC - Key Value Coding for Erlang data structures
=================================================

<bob@redivi.com>

Overview:
---------

kvc supports Key Value Coding-like queries on common Erlang data structures.
A common use case for kvc is to quickly access one or more deep values in
decoded JSON, or some other nested data structure. It can also help with some
aggregate operations. It solves similar problems that you might want to
use a tool like XPath or jQuery for, but it is far simpler but strictly less
powerful.

The following common Erlang data structures are supported:

* `list()`
* `dict()`
* `gb_trees()`
* `proplist()`
* `{struct, proplist()}`

Only the following data types are permitted for keys, and they must be UTF-8
if any type coercion takes place:

* `atom()`
* `binary()`
* `string()`

Another limitation is that it is assumed that the given data structure has a
homogeneous key type. For example, if any key is `binary()`, all keys should
be `binary()`.

Status:
-------

Not used in production, but it has a test suite that passes.

Usage:
------

`proplist()`:
<code>
wibble =:= kvc:path(foo.bar.baz, [{foo, [{bar, [{baz, wibble}]}]}]).
</code>

mochijson2 `{struct, proplist()}` example:
<code>
<<"wibble">> =:= kvc:path(foo.bar.baz,
                     {struct,
                      [{<<"foo">>,
                        {struct,
                         [{<<"bar">>,
                           {struct, [{<<"baz">>, <<"wibble">>}]}}]}}]}).
</code>

mochijson2 `{struct, proplist()}` example:
<code>
<<"wibble">> =:= kvc:path(foo.bar.baz,
                     {struct,
                      [{<<"foo">>,
                        {struct,
                         [{<<"bar">>,
                           {struct, [{<<"baz">>, <<"wibble">>}]}}]}}]}).
</code>