# Networking and sockets using rust

just exploring how socket and networking works.

## Network sockets

Connect two machine on the internet.

![Socket Flow](/assets/socket-flow.png)

A little explanation from me:

### The Server

1. creates a [socket](https://www.man7.org/linux/man-pages/man2/socket.2.html)
file descriptor.

2. [bind](https://man7.org/linux/man-pages/man2/bind.2.html)
this socket file descriptor to some address
    > Different protocol families have their own ways of defining endpoint addresses.
    This means the address format can vary depending on the address family,
    allowing sockets to handle different networking protocols and address
    formats properly.

3. [listen](https://man7.org/linux/man-pages/man2/listen.2.html) for
incoming connections using the socket file descriptor

4. creating connection file descriptor using [accept](https://man7.org/linux/man-pages/man2/accept.2.html)
from the socket file descriptor we have created.

5. read the data from the client using [recv](https://man7.org/linux/man-pages/man2/recv.2.html)
or [read](https://man7.org/linux/man-pages/man2/read.2.html) it returns
how many bytes has been read.
    > The only difference between recv() and read(s) is the presence of
      flags.  With a zero flags argument, recv() is generally
      equivalent to read(2)

6. we can write back to the client using [send](https://man7.org/linux/man-pages/man2/sendto.2.html)
or [write](https://man7.org/linux/man-pages/man2/write.2.html)
    > The only difference between send() and write(2) is the presence of
      flags. With a zero flags argument, send() is equivalent to
      write(2).

7. use [close](https://man7.org/linux/man-pages/man2/close.2.html) to close
the connection file descriptor if we are done with this connection.
or close the socket descriptor if we need to close the server.

### The Client

1. creates a [socket](https://www.man7.org/linux/man-pages/man2/socket.2.html)
file descriptor.

2. [connect](https://man7.org/linux/man-pages/man2/connect.2.html) to some
address using the socket file descriptor.

3. we can write to the server using [send](https://man7.org/linux/man-pages/man2/sendto.2.html)
or [write](https://man7.org/linux/man-pages/man2/write.2.html)
    > The only difference between send() and write(2) is the presence of
      flags. With a zero flags argument, send() is equivalent to
      write(2).

4. read the data from the server using [recv](https://man7.org/linux/man-pages/man2/recv.2.html)
or [read](https://man7.org/linux/man-pages/man2/read.2.html) it returns
how many bytes has been read.
    > The only difference between recv() and read(s) is the presence of
      flags.  With a zero flags argument, recv() is generally
      equivalent to read(2)

5. use [close](https://man7.org/linux/man-pages/man2/close.2.html) to close
 the socket file descriptor if we need to close the connection.

## Unix domain sockets

Connect two process/service on the same machine.
for example docker uses it but it put http server on top of it.
[docker.sock](https://stackoverflow.com/a/35110344)

![Container communcation](/assets/container-com.png)

## Resource

[Getting Started with Networking and Sockets](https://www.kungfudev.com/blog/2024/06/07/getting-started-with-net-and-sockets)
[Understanding Unix Domain Sockets in Golang](https://www.kungfudev.com/blog/2022/12/05/understanding-unix-domain-sockets-in-golang)
