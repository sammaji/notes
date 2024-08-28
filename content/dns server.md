- I used [this guide](https://github.com/EmilHernvall/dnsguide) (written in rust) to learn how to create a dns server.
- Here's my own [implementation](https://github.com/sammaji/toy-dns-server) of a dns resolver (written in typescript).

dns -> domain name system
### Send and receive UDP packets

Create a UDP socket that listens to port 2053.

```
const udpSocket = dgram.createSocket("udp4");
udpSocket.bind(2053, '127.0.0.1')
```

Then you can listen to events like `error`, `message`, `close`, etc.

```
udpSocket.on("message", (msg, rinfo) => {
	// listen to recieved messages
})
```

`rinfo` is remote info which contains information about the server sending the message

You can also messages using the `send()` method.

```
udpSocket.send(...)
```

### Parts of a dns server

All communications in the DNS protocol are carried in a single format called a "message". Each message consists of 5 sections: 
1. header -> information about query / response
2. question -> request for information about query name (domain) and record type
3. answer -> relevant records of the requested type
5. authority -> list of name servers (for recursive resolve), and
6. an additional space

#### Header section

The header section of a DNS message contains the following fields:

| Field                             | Size    | Description                                                                                   |
| --------------------------------- | ------- | --------------------------------------------------------------------------------------------- |
| Packet Identifier (ID)            | 16 bits | A random ID assigned to query packets. Response packets must reply with the same ID. <br>     |
| Query/Response Indicator (QR)     | 1 bit   | 1 for a reply packet, 0 for a question packet.  <br>                                          |
| Operation Code (OPCODE)           | 4 bits  | Specifies the kind of query in a message.  <br>                                               |
| Authoritative Answer (AA)         | 1 bit   | 1 if the responding server "owns" the domain queried, i.e., it's authoritative.  <br>         |
| Truncation (TC)                   | 1 bit   | 1 if the message is larger than 512 bytes. Always 0 in UDP responses.  <br>                   |
| Recursion Desired (RD)            | 1 bit   | Sender sets this to 1 if the server should recursively resolve this query, 0 otherwise.  <br> |
| Recursion Available (RA)          | 1 bit   | Server sets this to 1 to indicate that recursion is available.  <br>                          |
| Reserved (Z)                      | 3 bits  | Used by DNSSEC queries. At inception, it was reserved for future use.  <br>                   |
| Response Code (RCODE)             | 4 bits  | Response code indicating the status of the response.  <br>                                    |
| Question Count (QDCOUNT)          | 16 bits | Number of questions in the Question section.  <br>                                            |
| Answer Record Count (ANCOUNT)     | 16 bits | Number of records in the Answer section.  <br>                                                |
| Authority Record Count (NSCOUNT)  | 16 bits | Number of records in the Authority section.  <br>                                             |
| Additional Record Count (ARCOUNT) | 16 bits | Number of records in the Additional section.  <br>                                            |
The header section is always 12 bytes long. Integers are encoded in big-endian format.

#### Storing flags in a bit mask

```
const flags = 
	(qr << 15) | 
	(opcode << 11) |
	(aa << 10) |
	(tc << 9) |
	(rd << 8) |
	(ra << 7) |
	(z << 4) |
	rcode;
```

#### Retrieving flags

```
const readflags = (flags: number): HeaderFlagParams => {
  const qr = (flags >> 15) & 0b1;
  const opcode = (flags >> 11) & 0b1111;
  const aa = (flags >> 10) & 0b1;
  const tc = (flags >> 9) & 0b1;
  const rd = (flags >> 8) & 0b1;
  const ra = (flags >> 7) & 0b1;
  const z = (flags >> 4) & 0b111;
  const rcode = flags & 0b1111;
  return { qr, opcode, aa, tc, rd, ra, z, rcode };
};
```

### Question section

The question section contains a list of questions (usually just 1) that the sender wants to ask the receiver. This section is present in both query and reply packets.

Each question has the following structure:

- **Name**: A domain name, represented as a sequence of "labels" (more on this below)
- **Type**: 2-byte int; the type of record (1 for an A record, 5 for a CNAME record etc., full list [here](https://www.rfc-editor.org/rfc/rfc1035#section-3.2.2))
- **Class**: 2-byte int; usually set to `1` (full list [here](https://www.rfc-editor.org/rfc/rfc1035#section-3.2.4))

#### Answer section

The answer section contains a list of RRs (Resource Records), which are answers to the questions asked in the question section.

Each RR has the following structure:

|Field|Type|Description|
|---|---|---|
|Name|Label Sequence|The domain name encoded as a sequence of labels.|
|Type|2-byte Integer|`1` for an A record, `5` for a CNAME record etc., full list [here](https://www.rfc-editor.org/rfc/rfc1035#section-3.2.2)|
|Class|2-byte Integer|Usually set to `1` (full list [here](https://www.rfc-editor.org/rfc/rfc1035#section-3.2.4))|
|TTL (Time-To-Live)|4-byte Integer|The duration in seconds a record can be cached before requerying.|
|Length (`RDLENGTH`)|2-byte Integer|Length of the RDATA field in bytes.|
|Data (`RDATA`)|Variable|Data specific to the record type.|

[Section 3.2.1](https://www.rfc-editor.org/rfc/rfc1035#section-3.2.1) of the RFC covers the answer section format in detail.

In this stage, we'll only deal with the "A" record type, which maps a domain name to an IPv4 address. The RDATA field for an "A" record type is a 4-byte integer representing the IPv4 address.

### [[Header compression]]

## Dns Server
A dns server is generally either of these two types:
### Authoritative server
A dns server hosting one or more zones. Its the final holder of the IP address of the domain you are looking for.

For example, the authoritative servers for the zone google.com are ns1.google.com, ns2.google.com, ns3.google.com and ns4.google.com.

### Caching Server
Caching Server - A DNS server that services DNS lookups by first checking its cache to see if it already knows of the record being requested, and if not performing a recursive lookup to figure it out.
## [[Recursive Resolve]]