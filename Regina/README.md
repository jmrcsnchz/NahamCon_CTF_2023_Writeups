# Regina [Warmup]

NahamCon CTF 2023

*I have a tyrannosaurus rex plushie and I named it Regina! Here, you can talk to it :)*

## Writeup

```bash
$ ssh -p 31958 user@challenge.nahamcon.com                                          Sun 18 Jun 2023 07:39:51 AM EDT

The authenticity of host '[challenge.nahamcon.com]:31958 ([34.29.202.81]:31958)' can't be established.
ED25519 key fingerprint is SHA256:RXVB5w2/rnBHSJwJzSaOXmLy+UM0zNPzcHHHqra3R2Q.
This host key is known by the following other names/addresses:
    ~/.ssh/known_hosts:171: [hashed name]
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '[challenge.nahamcon.com]:31958' (ED25519) to the list of known hosts.
user@challenge.nahamcon.com's password: 

/usr/local/bin/regina: REXX-Regina_3.9.4(MT) 5.00 25 Oct 2021 (64 bit)


```

SSH Session is directed to Regina binary. Read contents of flag.txt with a Rexx command

```bash
$ echo "say linein('flag.txt')" | ssh -p 31958 user@challenge.nahamcon.com      
```

Output:
```
Pseudo-terminal will not be allocated because stdin is not a terminal.
user@challenge.nahamcon.com's password: 

/usr/local/bin/regina: REXX-Regina_3.9.4(MT) 5.00 25 Oct 2021 (64 bit)
flag{2459b9ae7c704979948318cd2f47dfd6}
```
