---
title: Socks5 协议
date: 2015-11-26
---


http://www.ietf.org/rfc/rfc1928.txt

## Connect

#### Client

    +----+----------+----------+
    |VER | NMETHODS | METHODS  |
    +----+----------+----------+
    | 1  |    1     | 1 to 255 |
    +----+----------+----------+

    - VER       protocol version: X'05'
    - NMETHODS  the length of methods
    - METHODS
        - X'00' NO AUTHENTICATION REQUIRED
        - X'01' GSSAPI
        - X'02' USERNAME/PASSWORD
        - X'03' to X'7F' IANA ASSIGNED
        - X'80' to X'FE' RESERVED FOR PRIVATE METHODS
        - X'FF' NO ACCEPTABLE METHODS


#### Server

    +----+--------+
    |VER | METHOD |
    +----+--------+
    | 1  |   1    |
    +----+--------+

    - VER       X'05' SOCKS5
    - METHOD    one of the methods given in METHODS

    If the selected METHOD is X'FF', none of the methods listed by the
    client are acceptable, and the client MUST close the connection.

    The client and server then enter a method-specific sub-negotiation.

## Addressing

#### Client

    +----+-----+-------+------+----------+----------+
    |VER | CMD |  RSV  | ATYP | DST.ADDR | DST.PORT |
    +----+-----+-------+------+----------+----------+
    | 1  |  1  | X'00' |  1   | Variable |    2     |
    +----+-----+-------+------+----------+----------+

    - VER protocol version: X'05'
    - CMD
        - CONNECT X'01'
        - BIND X'02'
        - UDP ASSOCIATE X'03'
    - RSV    RESERVED
    - ATYP   address type of following address
        - IP V4 address: X'01'
        - DOMAINNAME: X'03'
        - IP V6 address: X'04'
    - DST.ADDR desired destination address
    - DST.PORT desired destination port in network octet order

    - ATYP and DST.ADDR
        - X'01' IPv4
            DST.ADDR 4字节
        - X'03' Host
            +---------------+----------+
            |length of host |   host   |
            +---------------+----------+
            |       1       | Variable |
            +---------------+----------+
        - X'04' IPv6
            DST.ADDR 16字节

#### Server

        +----+-----+-------+------+----------+----------+
        |VER | REP |  RSV  | ATYP | BND.ADDR | BND.PORT |
        +----+-----+-------+------+----------+----------+
        | 1  |  1  | X'00' |  1   | Variable |    2     |
        +----+-----+-------+------+----------+----------+

        - VER    protocol version: X'05'
        - REP    Reply field:
           - X'00' succeeded
           - X'01' general SOCKS server failure
           - X'02' connection not allowed by ruleset
           - X'03' Network unreachable
           - X'04' Host unreachable
           - X'05' Connection refused
           - X'06' TTL expired
           - X'07' Command not supported
           - X'08' Address type not supported
           - X'09' to X'FF' unassigned
        - RSV    RESERVED, must be set to X'00'
        - ATYP   address type of following address
            - IP V4 address: X'01'
            - DOMAINNAME: X'03'
            - IP V6 address: X'04'
         - BND.ADDR server bound address
         - BND.PORT server bound port in network octet order

CONNECT

    In the reply to a CONNECT, BND.PORT contains the port number that the
    server assigned to connect to the target host, while BND.ADDR
    contains the associated IP address. 

BIND

    The BIND request is used in protocols which require the client to
    accept connections from the server.

    Two replies are sent from the SOCKS server to the client during a
    BIND operation.  

    The first is sent after the server creates and binds
    a new socket.  The BND.PORT field contains the port number that the
    SOCKS server assigned to listen for an incoming connection.  The
    BND.ADDR field contains the associated IP address.  

    The second reply occurs only after the anticipated incoming
    connection succeeds or fails.
    In the second reply, the BND.PORT and BND.ADDR fields contain the
    address and port number of the connecting host.

UDP ASSOCIATE

    The UDP ASSOCIATE request is used to establish an association within
    the UDP relay process to handle UDP datagrams.  The DST.ADDR and
    DST.PORT fields contain the address and port that the client expects
    to use to send UDP datagrams on for the association.  

    In the reply to a UDP ASSOCIATE request, the BND.PORT and BND.ADDR
    fields indicate the port number/address where the client MUST send
    UDP request messages to be relayed.

## Reply Processing

    When a reply (REP value other than X'00') indicates a failure, the
    SOCKS server MUST terminate the TCP connection shortly after sending
    the reply.  This must be no more than 10 seconds after detecting the
    condition that caused a failure.

    If the reply code (REP value of X'00') indicates a success, and the
    request was either a BIND or a CONNECT, the client may now start
    passing data.

## Procedure for UDP-based clients

    A UDP-based client MUST send its datagrams to the UDP relay server at
    the UDP port indicated by BND.PORT in the reply to the UDP ASSOCIATE
    request. Each UDP datagram carries a UDP request.

    +----+------+------+----------+----------+----------+
    |RSV | FRAG | ATYP | DST.ADDR | DST.PORT |   DATA   |
    +----+------+------+----------+----------+----------+
    | 2  |  1   |  1   | Variable |    2     | Variable |
    +----+------+------+----------+----------+----------+

    - RSV  Reserved X'0000'
    - FRAG    Current fragment number
    - ATYP    address type of following addresses:
       - IP V4 address: X'01'
       - DOMAINNAME: X'03'
       - IP V6 address: X'04'
    - DST.ADDR       desired destination address
    - DST.PORT       desired destination port
    - DATA     user data

    When a UDP relay server decides to relay a UDP datagram, it does so
    silently, without any notification to the requesting client.
    Similarly, it will drop datagrams it cannot or will not relay.

    The UDP relay server MUST acquire from the SOCKS server the expected
    IP address of the client that will send datagrams to the BND.PORT
    given in the reply to UDP ASSOCIATE.  It MUST drop any datagrams
    arriving from any source IP address other than the one recorded for
    the particular association.

    The FRAG field indicates whether or not this datagram is one of a
    number of fragments.  If implemented, the high-order bit indicates
    end-of-fragment sequence, while a value of X'00' indicates that this
    datagram is standalone.  Values between 1 and 127 indicate the
    fragment position within a fragment sequence.  Each receiver will
    have a REASSEMBLY QUEUE and a REASSEMBLY TIMER associated with these
    fragments.  The reassembly queue must be reinitialized and the
    associated fragments abandoned whenever the REASSEMBLY TIMER expires,
    or a new datagram arrives carrying a FRAG field whose value is less
    than the highest FRAG value processed for this fragment sequence.
    The reassembly timer MUST be no less than 5 seconds.  It is
    recommended that fragmentation be avoided by applications wherever
    possible.

    Implementation of fragmentation is optional; an implementation that
    does not support fragmentation MUST drop any datagram whose FRAG
    field is other than X'00'.


    The programming interface for a SOCKS-aware UDP MUST report an
    available buffer space for UDP datagrams that is smaller than the
    actual space provided by the operating system:

    - if ATYP is X'01' - 10+method_dependent octets smaller
    - if ATYP is X'03' - 262+method_dependent octets smaller
    - if ATYP is X'04' - 20+method_dependent octets smaller

