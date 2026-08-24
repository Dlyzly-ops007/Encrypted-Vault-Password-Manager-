# password-manager

A CLI password manager with an encrypted local vault. Entries are encrypted at rest using a key derived from your master password — nothing is stored in plaintext.

## How it works

- A single master password unlocks the vault (never stored, only used to derive a key).
- Key derivation: PBKDF2-HMAC-SHA256, 100,000 iterations, per-vault random salt (`salt.bin`).
- Vault contents are encrypted with Fernet (symmetric AES) and stored in `vault.enc`.
- First run creates the vault; every run after that unlocks it with the master password.

## Features

- Add an entry (manual password or a generated strong one)
- View all stored entries
- Edit an existing entry (update username and/or password, keep or regenerate the password)
- Delete an entry
- Password generator: configurable length, mixes letters, digits, and punctuation via `secrets` (cryptographically secure)
- Auto-saves the vault after every change; vault re-encrypts and locks on exit

## Setup

```bash
pip install -r requirements.txt
python password_manager.py
```

On first run you'll be asked to set a master password — this creates `salt.bin` and `vault.enc` in the working directory. Keep both files; losing `salt.bin` makes the vault unrecoverable, even with the correct password.

## Usage

```
==== PASSWORD MANAGER ====
1. Add entry
2. View entries
3. Edit entry
4. Delete entry
5. Exit (Lock vault)
```

## Notes

- `vault.enc` and `salt.bin` are gitignored — don't commit real vault data.
- This is a learning/portfolio project, not an audited production password manager. Don't use it as your only password store for real accounts.

## License

PolyForm Noncommercial 1.0.0 — see [LICENSE](LICENSE). Free for personal, educational, and noncommercial use.
