# Tarik ESSARHIR — Public PKI

This repository contains the public certificates associated with my personal cryptographic identity and YubiKey.

Private keys are not stored in this repository.

## Root CA

**Name:** Tarik ESSARHIR Personal CA
**Purpose:** Personal PKI trust anchor
**Certificate:** [`ca/tarik-personal-ca.crt`](ca/tarik-personal-ca.crt)

**SHA-256 fingerprint:**

`5B:77:47:98:31:F1:78:53:5A:23:13:EA:75:1A:E7:09:C1:06:31:BF:B1:EB:CE:56:4B:0C:AC:3C:4B:2F:1F:E3`

> Trusting this CA is a decision that must be made independently by the relying party. Publication in this repository does not constitute certification by a publicly trusted Certificate Authority.

## YubiKey Certificates

### PIV 9a — Authentication

**Purpose:** Authentication
**Algorithm:** ECC P-256
**Certificate:** [`certificates/9a-authentication.pem`](certificates/9a-authentication.pem)

**SHA-256 fingerprint:**

`8A:87:F6:CF:B9:4D:8E:B3:88:A4:76:26:8C:74:B8:85:EC:C8:FF:44:16:1B:4E:08:7C:D8:04:2C:43:E5:7E:CE`

### PIV 9c — Digital Signature

**Purpose:** Digital signatures and S/MIME signing
**Algorithm:** ECC P-256
**Identity:** Tarik ESSARHIR
**Email identities:**
- es.tarik@icloud.com
- essarhir.t@outlook.com

**Certificate:** [`certificates/9c-digital-signature.pem`](certificates/9c-digital-signature.pem)

**SHA-256 fingerprint:**

`4C:4F:C6:ED:77:6E:BE:36:BB:C8:BC:3A:DF:E1:5F:B9:D7:3F:36:1A:0E:BF:1A:16:80:2B:34:1A:47:C5:30:9C`

### PIV 9d — Key Management

**Purpose:** Key agreement / key management
**Algorithm:** ECC P-256
**Certificate:** [`certificates/9d-key-management.pem`](certificates/9d-key-management.pem)

**SHA-256 fingerprint:**

`2C:76:FA:01:D3:60:F6:82:ED:99:AB:61:7B:17:11:99:FD:C7:2F:B0:49:0B:60:0B:46:C6:07:BC:C7:62:72:E1`

## Certificate Architecture

The certificates published in this repository are issued by my personal CA:

    Tarik ESSARHIR Personal CA
                 │
        ┌────────┼────────┐
        │        │        │
       9a       9c       9d
      Auth    Signing    Key
                        Management

Each PIV slot uses a distinct ECC P-256 private key.

The corresponding private keys are hardware-protected and remain on my YubiKey.

## Historical Record

This repository also serves as a public historical record of my certificates.

When a certificate is renewed, replaced, or retired, its public certificate may be retained in the `archive/` directory rather than removed.

Git history provides an additional historical record of certificate publication and changes.

Git/GitHub history should not be interpreted as a trusted or qualified timestamping service.

## Verification

The SHA-256 fingerprint of a certificate can be calculated using OpenSSL:

    openssl x509 -in certificate.pem -noout -fingerprint -sha256

For identity-sensitive verification, fingerprints should preferably be compared against a copy obtained through an independent trusted channel.

## Trust Model

These certificates are issued by a personal Certificate Authority and are therefore not automatically trusted by operating systems, browsers, PDF readers, or email clients.

A relying party may explicitly trust the root certificate:

`ca/tarik-personal-ca.crt`

after independently verifying its fingerprint.

Publication of these certificates allows cryptographic keys and signatures to be compared against the public historical record, but does not by itself constitute third-party identity certification.

## Security

This repository contains **public cryptographic material only**.

It does **not** contain:

- Private keys
- CA private keys
- YubiKey PINs or PUKs
- PIV Management Keys
- Recovery secrets

The private key corresponding to each YubiKey certificate is not published.
