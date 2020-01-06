# modules

## securerandom

[SecureRandomモジュール 概要](https://docs.ruby-lang.org/ja/latest/class/SecureRandom.html
)

```rb
$ irb
>> require 'securerandom'
=> true
>> SecureRandom.hex(8)
=> "4f94456a1a0c5d00"
>> SecureRandom.alphanumeric(8)
=> "8PWuk93k"
```

### hex

ランダムな hex (16進数) 文字列を生成して返す. RETURN: 0-9、A-F.

### alphanumeric

ランダムな英数字を生成して返す. RETURN: 0-9、a-z, A-Z.
