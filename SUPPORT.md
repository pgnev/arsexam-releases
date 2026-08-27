# ArsExam Support

## Official contact

**petkoganev@gmail.com**

For normal product support, prefer the in-application **Help → Contact support** flow when it is available in the installed version.

## What to include

A useful support request should contain only the minimum information necessary to investigate the case:

- ArsExam version and distribution mode (Desktop/Portable);
- a short description of the problem;
- exact steps that reproduce it;
- the exact error text shown by ArsExam, when relevant;
- a minimal privacy-safe diagnostic/support bundle only when relevant and intentionally attached by the user.

## Do not send

Do **not** send by e-mail:

- plaintext profile passwords;
- Recovery Keys;
- Backup passwords;
- Transfer codes;
- complete databases or full Backup archives unless a specific support case strictly requires one and a safe transfer method has been agreed;
- confidential examination content that is not strictly required;
- signing material, API keys or unrelated credentials;
- unrelated personal data.

ArsExam support should never ask for your old plaintext password, Recovery Key, Backup password or Transfer code.

## Password recovery in ArsExam 3.2.0

Forgotten-password recovery is **local** and uses the active Recovery Key for the profile.

ArsExam 3.2.0 does **not** use:

- Supabase password recovery;
- recovery e-mail enrollment;
- Request ID;
- support-issued reset codes;
- a universal server-side/master password.

After a successful recovery, the old password and the Recovery Key used for that recovery become invalid, and a new Recovery Key is generated.

For new 3.2+ profiles, the active Recovery Key can also be kept in an encrypted profile-bound local vault. If the user still knows the current profile password, ArsExam can authenticate the user and show/re-export the active key from **Settings → Password and recovery**. Older profiles without a Recovery Key vault may require one authenticated Recovery Key replacement before this management capability is available.

If both the current profile password and the valid Recovery Key are lost, support has no hidden bypass capable of unlocking the profile.

## Backup and Transfer assistance

A Backup password is specific to its Backup and is not interchangeable with the profile password or Recovery Key. A Transfer code is temporary and is not a password-recovery credential.

When reporting Backup/Restore/Transfer problems, include identifiers and status/error text where useful, but do not send the secret credentials themselves.

## Security reports

Suspected security vulnerabilities should be reported privately to the same contact with subject `ArsExam security report`. Do not publish exploitable details in a public GitHub issue. See `SECURITY.md`.

## Availability

Support is provided according to available capacity and is not a guaranteed service-level agreement unless explicitly agreed in writing.
