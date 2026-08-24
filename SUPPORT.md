# ArsExam Support

## Official contact

**petkoganev@gmail.com**

For normal product support, prefer the in-application **Help → Contact support** flow when it is available in the installed version. It can include the ArsExam version/distribution context and a support identifier without automatically exposing examination content.

## What to include

A useful support request should contain only the minimum information necessary to investigate the case:

- ArsExam version and distribution mode (Desktop/Portable);
- a short description of the problem;
- exact steps that reproduce it;
- the error text shown by ArsExam, when relevant;
- a minimal privacy-safe diagnostic/support bundle only when relevant and intentionally attached by the user.

## Do not send

Do **not** send by e-mail:

- plaintext passwords;
- Recovery Kits or recovery secrets;
- complete databases;
- full examination-bank archives;
- confidential examination content that is not strictly required for the case;
- signing material, API keys or credentials;
- unrelated personal data.

ArsExam support should never ask for your old plaintext password.

## Password recovery

Password-recovery capabilities depend on the installed ArsExam version.

In a version where **secure support-assisted online recovery** is enabled, the user must first enroll a recovery e-mail while signed in and after confirming the current ArsExam password. The recovery service stores a SHA-256 hash of the normalized address rather than the plaintext mailbox address.

For a later forgotten-password request:

1. ArsExam creates an opaque, time-limited Request ID only if that installation already has an enrolled recovery contact.
2. The user provides the Request ID and the previously enrolled recovery e-mail to support.
3. The trusted backend compares a server-side hash of the supplied address with the pre-enrolled hash.
4. If they do not match, **no reset code is issued**.
5. If they match, the one-time code must be sent **only to that same pre-enrolled mailbox**.

A Request ID is **not proof of identity**. Knowledge of the e-mail address is also not sufficient by itself; the requester must be able to receive the one-time code at the pre-enrolled mailbox.

Support must not send a recovery code to a new/alternative address supplied only during the forgotten-password request. If the user no longer controls the enrolled mailbox, the normal forgot-password flow must fail closed and any contact-change request must be handled as a separate exceptional support case.

Legacy Recovery Kit material must not be sent casually by e-mail and must not be requested as a substitute for this recovery procedure.

## Security reports

Suspected security vulnerabilities should be reported privately to the same contact with a clear subject such as `ArsExam security report`. Do not publish exploitable details in a public GitHub issue. See `SECURITY.md`.

## Availability

Support is provided according to available capacity and is not a guaranteed service-level agreement unless explicitly agreed in writing.
