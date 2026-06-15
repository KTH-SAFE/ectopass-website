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
