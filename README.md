# `cbor-deterministic` gem

Use with the [`cbor`][cbor-ruby] gem (or with `cbor-pure`, which is a
part of the [`cbor-diag`][cbor-diag] gem) to
add a `to_deterministic_cbor` method on objects.
Requires `to_cbor` to already be mostly deterministic (as it is for the
above two [CBOR] implementations), just adds deterministic ordering of maps
for completeness.

Note that this implements deterministic encoding as in [Section 4.2 of
RFC 8949](https://www.rfc-editor.org/rfc/rfc8949.html#section-4.2).
An earlier variant of this, [Length-First Map Key
Ordering](https://www.rfc-editor.org/rfc/rfc8949.html#section-4.2.3),
was previously called "canonical encoding" ([Section 3.9 of RFC
7049](https://www.rfc-editor.org/rfc/rfc7049.html#section-3.9)) and is
still available as the analogously shaped `cbor-canonical` gem.

```ruby
require 'cbor-deterministic'

ex1 = {[]=> 1, aa: 2}

p CBOR.decode(ex1.to_cbor)
# {[]=>1, "aa"=>2}

p CBOR.decode(ex1.to_deterministic_cbor)
# {"aa"=>2, []=>1}
```

[cbor-ruby]: https://github.com/cabo/cbor-ruby
[cbor-diag]: https://github.com/cabo/cbor-diag
[CBOR]: http://cbor.io
