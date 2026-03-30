# libfoxenflac-x68k

libfoxenflac FLAC decoder library for x68k

軽量FLAC decoderライブラリのlibfoxenflacをX68k向けに最適化し、elf2x68kでビルドしたものになります。

680x0の不得意な64bit乗算をなるべく行わないようにするとともに、最終的にまーきゅりーゆにっとで鳴らすことを前提に、16bitステレオインターリーブのデータを直接出力するようにして高速化してあります。

68000汎用/68030以上用/68060専用があります。


使う時は、サブモジュールとして組み込むのが簡単です。例えばプロジェクト直下にて以下を実行します。

```
git submodule add https://github.com/tantanGH/libfoxenflac-x68k.git libs/libfoxenflac-x68k
```

以下のようなツリーとなります。

```
my_app/
├── .git/
├── .gitmodules
├── libs/
│   └── libfoxenflac-x68k/
│       ├── include/flac.h
│       └── lib/libfoxenflac.a
└── src/
    ├── main.c
    └── Makefile
```

ヘッダー検索パスとライブラリ検索パスをMakefile内で
```
-I../libs/libfoxenflac-x68k/include
-L../libs/libfoxenflac-x68k/lib
```
のように指定し、`-lfoxenflac` でリンクできます。
68030以上用、68060専用はそれぞれ`-lfoxenflac030`,`-lfoxenflac060`としてください。

---

/*
 *  libfoxenflac -- Tiny FLAC Decoder Library
 *  Copyright (C) 2018-2022  Andreas Stöckel
 *
 *  This program is free software: you can redistribute it and/or modify
 *  it under the terms of the GNU General Public License as published by
 *  the Free Software Foundation; either version 2 of the License, or
 *  (at your option) any later version.
 *
 *  This program is distributed in the hope that it will be useful,
 *  but WITHOUT ANY WARRANTY; without even the implied warranty of
 *  MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
 *  GNU General Public License for more details.
 *
 *  You should have received a copy of the GNU General Public License
 *  along with this program.  If not, see <https://www.gnu.org/licenses/>.
 */
