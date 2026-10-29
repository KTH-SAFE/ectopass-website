+++
date = '2026-06-10T11:12:42+02:00'
draft = false
title = 'Benchmarks'
weight = 30
menu = "main"
+++

### Libsodium

[Libsodium](https://libsodium.gitbook.io/doc) is a crypto library written in C.

We compared two versions of Libsodium:

- one where SLH is activated on all files
- one where SLH is activated only for files where Ectopass finds a vulnerability (selective SLH)

We observed that the overhead of SLH is significantly lower when SLH is applied selectively. Note
that this is without using any annotation in Ectopass' configuration to remove eventual false positives.
The difference could be even higher using them.

| Mitigation | Average Overhead |
| ---------- | ---------------- |
| SLH | 831% |
| Selective SLH | 4% |

![libsodium results](/static/images/libsodium.png)

### nginx

[nginx](https://nginx.org/) is a very popular web server written in C.

To benchmark it, we configured it with HTTPS (with a locally signed certificate) and linked it with a locally compiled OpenSSL library.
We first noticed that enabling or disabling SLH on all files for nginx alone did not change much the results so in this
benchmark we only used a version of nginx with selective SLH.
We can observe a noticeable difference in the results if OpenSSL is compiled with or without SLH.

To benchmark the web server we ran 400000 requests with 10 concurrent threads to get the Ectopass tutorial page:

```
ab -n 400000 -c 10 https://localhost:1312/tutorial/
```

We used the number of requests per second to estimate overhead. We get the following results.

Note that for this benchmark, instead of activating SLH for whole files we active it only on vulnerable functions.
This greatly reduces the scope of the code which would contain performance overhead.

| Mitigation for OpenSSL | Request rate (#/sec) | Overhead |
| ---------- | ---------------- | ---------------- |
| No SLH | 1558.15 | 0% |
| Selective SLH | 1536.05 | 1.43% |
| SLH | 1359.10 | 13.64% |
