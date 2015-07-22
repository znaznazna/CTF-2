1. 使用`ext_interactive`交互输入不可见字符：

	```python
	>>> from pwn import *
	>>> from utils import *
	>>> io = process('cat')
	[+] Started program 'cat'
	>>> io.sendline('0\x30 A\x41')
	>>> io.recvline(False)
	'00 AA'
	>>> io.ext_interactive()
	[*] Switching to extensive interactive mode
	A\x410\x30
	AA00
	```

2. 使用`gdb`调试程序：

	```python
	>>> from pwn import *
	>>> from utils import *
	>>> io = debug('cat')
	[x] Starting program '/usr/local/bin/gdb' argv=['gdb', 'cat'] 
	>>> # io.b('main') <=> io.sendline('b main')
	>>> # io.b(0x08040000) <=> io.sendline('b * 0x08040000')
	>>> # io.c() <=> io.sendline('c')
	>>> io.r() # <=> io.sendline('r')
	>>> io.ext_interactive()
	[*] Switching to extensive interactive mode
	Reading symbols from cat...(no debugging symbols found)...done.
	### Pressed ctrl+c here in order to interrupt the running program ###
	Program received signal SIGINT, Interrupt.
	...
	Stopped reason: SIGINT
	gdb$ i prog
	gdb$ c
	Continuing.
	### input c! <=> exit interactive mode and run io.c() ###