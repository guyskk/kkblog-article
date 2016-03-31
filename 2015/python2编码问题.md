---
title: Python2 编码问题
date: 2015-04-15
---


系统默认编码

    sys.getdefaultencoding()

文件系统编码/路径名，文件名之类的

    sys.getfilesystemencoding()

标准输入输出编码，取决于使用的 shell

    sys.stdin.encoding
    sys.stdout.encoding

这样也可以

    import locale
    import codecs
    print locale.getpreferredencoding();
    print codecs.lookup(locale.getpreferredencoding()).name

## ``coding:utf-8`` 和 ``u''``

代码如下

	#coding:utf-8

	u=u'中文'
	s='中文'
	print u
	print s

1. 代码文件开头加上 `#coding:utf-8`，代码中有中文字符，文件用 utf-8 编码保存，一切正常。

2. 代码文件开头加上 `#coding:utf-8`，代码中有中文字符，文件用 gbk 编码保存，报错 `SyntaxError: (unicode error) 'utf8' codec can't decode byte 0xd6 in position 0: invalid continuation byte`

3. 代码文件开头无 `#coding:utf-8`，代码中有中文字符，文件用 utf-8 编码保存，报错 `SyntaxError: Non-ASCII character '\xd6' in file`

4. 代码文件开头无 `#coding:utf-8`，代码中有中文字符，文件用 gbk 编码保存，报错 `SyntaxError: Non-ASCII character '\xd6' in file`

## str 与 unicode

假设代码文件开头加上 `#coding:utf-8`，代码中有中文字符，文件用 utf-8 编码保存。控制台可以显示 utf-8 编码的字符。

1. `u=u'中文'`，u 是 unicode 类型。

2. `u=u'中文'`，u.encode('utf-8') 是 str 类型,编码格式是 utf-8。

3. `u=u'中文'`，u.encode('gbk') 是 str 类型，编码格式是 gbk。

4. `u=u'中文'`，u.encode("ascii") 报错 `UnicodeEncodeError: 'ascii' codec can't encode characters in position 0-1: ordinal not in range(128)`，ascii 编码无法保存中文字符。

5. `u=u'中文'`，u.decode('utf-8')，u.decode("gbk")，u.decode("ascii") 报错 `UnicodeEncodeError: 'ascii' codec can't encode characters in position 0-1: ordinal not in range(128)`。

--------------------------

1. `s='中文'`, s 是 str 类型，编码格式是 utf-8。

2. `s='中文'`, s.decode('utf-8') 是 unicode 类型。

3. `s='中文'`, s.decode('gbk') 报错 `UnicodeDecodeError: 'gbk' codec can't decode bytes in position 2-3: illegal multibyte sequence`。

4. `s='中文'`, s.decode("utf-16") 是 unicode 类型，但是内容已经乱码。

5. `s='中文'`, s.encode('gbk')，s.encode('utf-8')，s.encode('ascii')，s.encode('utf-16') 报错 `UnicodeDecodeError: 'ascii' codec can't decode byte 0xe4 in position 0: ordinal not in range(128)`。

## 总结：

- unicode 类型通过 encode() 方法用指定编码转成 str 类型，此时可以储存到磁盘或数据库。

- str 类型通过 decode() 方法用指定编码转成 unicode 类型，若指定编码和 str 的编码一致，此时可以使用这些字符；若不一致，则可能报错或者出现乱码。

- str.decode(原编码).encode(目标编码)，这样将 str 字符用目标编码保存。