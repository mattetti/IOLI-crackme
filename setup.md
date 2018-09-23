# Setup

You might be interested in playing with thos crackmes coming from [radare](https://rada.re/r/).

But you know very well that running untrusted binaries on your machine is a terrible idea. Thankfully there is a good solution for that: Docker!

## Docker

install [docker](https://www.docker.com/get-started)

Pull the latest image:

```
docker pull radare/radare2
```

Build a container:

```
docker build -t crackme .
```

Mount the files locally and run the container while connecting to a shell:

```
 docker run -ti --cap-drop=ALL --cap-add=SYS_PTRACE -v "$(pwd)"/bin-linux:/crackme radare/radare2:latest
```

You can now execute the executable safely:

```
cd crackme
./crackme0x00
```

And run radare:

```
r2 -AAwd crackme0x00
```

```
[0x08048360]> pdf @ main
```

or the other tools:

```
rabin2 -z ./crackme0x00
```

```
cp crackme0x02 crackme0x02-k
r2 -wAxd crackme0x02-k
pdf @ main
wa nop @ 0x08048451
q
./crackme0x02-k
```
