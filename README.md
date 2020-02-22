gpg-sae
=======

A little bash utility for signing and decrypting files

# Prerequisite or Helpful links

- [How to create a GPG key](https://help.github.com/en/github/authenticating-to-github/generating-a-new-gpg-key)
- [How to backup a GPG keyring](https://makandracards.com/makandra/37763-gpg-extract-private-key-and-import-on-different-machine)

# Usage

## Configuration

This utility was created to be as minimalist as possible, however, there
are a few configuration settings you can apply in your environment.

| Environment Variable                       | Description                                                                                            | Example                                     |
|--------------------------------------------|--------------------------------------------------------------------------------------------------------|---------------------------------------------|
| `GPG_KEY_ID`                               | YOUR primary key id to be used encrypt/decrypt functions. Used for gpg arg `(-r, --recipient USER-ID)` | `GPG_KEY_ID=CodyLane`                       |
| `DELETE_NON_ENCRYPTED_FILE_AFTER_ENCRYPT`  | When set to `Y` the default, the original file is deleted after encryption                             | `DELETE_NON_ENCRYPTED_FILE_AFTER_ENCRYPT=Y` |

## Example encrypting a file

- Creates an example file called `encrypt_this_file` that we will encrypt

```
cat > encrypt_this_file <<EOF
this is my special file that I would like to encrypt
EOF
```

- Ensure the file contains our text

#### `cat encrypt_this_file`

```
this is my special file that I would like to encrypt
```

- First we get a list of our keys and fingerprints

#### `gpg --list-keys`

```

/home/username/.gnupg/pubring.kbx
----------------------------------
pub   rsa4096 2020-02-22 [SC]
      123CB55F1237F1237123456789D12AC123E15123
uid           [ultimate] CodyLane <xxxxxxxx@example.com>
sub   rsa4096 2020-02-22 [E]

```

- Next we set `GPG_KEY_ID`

#### `GPG_KEY_ID=123CB55F1237F1237123456789D12AC123E15123 ./gpg-sae encrypt encrypt_this_file`

**OR**

#### `GPG_KEY_ID=CodyLane ./gpg-sae encrypt encrypt_this_file`

- Next we verify the original file has been deleted, and we have a new encrypted file

#### `ls -l encrypt_this_file*`

```
-rw-r--r-- 1 x 7 1747 Feb 22 00:00 encrypt_this_file.asc
```

#### `cat encrypt_this_file`

```
-----BEGIN PGP MESSAGE-----

hQIMAyGuJ0m4OrsUARAAmTLm3mVIDO/iG5hkY+S/TtdzpgspzfkR+4vOeZw76mmW
4k6JyQ7r2PlZY/mCHwIrw+b+CfL3FGeJ5INzatXH7y+6pOgOoFJ6a7Wjwog2yN85
Q0+J6gZ9fc0e9XLLRoIKOC7rC9S7WuHIsnpGzG8ZrdEzbpYmR+miaAlfCnXFOrlc
+qsn3H3YT1CtIOsko6Ei+HYLXzuDqP26y3QDIRBbeZNv5Tg3CnkllNqnoRvsCpgs
EcC1w0DsCGwIiBjmaO0U8/0KVFVH7gwg5hgigsYI519hJL66NEo42ukvXG20yQKI
ObZTQOyKZ2+wKLUzaOfuHDF1AWJaa+A1e5EGqDovyl66Y5km6D1L4pseEKqrGFLf
SvQCg9EYkz6PI0BLckVC9+qYukq4nS72WF+KFmyGb9AdrH0rZOQma5TlOkUvDgag
qZ5kx+MyMeV37cwYz3cHbLaTiXP+9jxk34wFgrxEa7TJ78CEgaCIzON/+RXmi1c1
X/gm0kWHP3b8qsux8da14RTTHcpS6FuEBQ+vjPVnR5piTyVxLIWeE0og4dL1YPzG
nzlWg2baPhQarMUc2a4mqeScbCsCjTpAcshgkXZdbwT5S0rMnRekac//DWO6lhN+
nFIavpi3YDIVA3dWfFLcbE4RrHAtQSBQELflVGTibtYXvSsFZ0PzPfnEVK/p9JvS
6QFezEo2QkEtSfMaq6nDfKoqN8QfJnRUVqeFIu//RerSReqdHyNwjbh4sIbJKceA
kOy9OcwFeFOhXtjjUO3k/b7C8bZn0uuAumjyjuV1jPyP299Yv06xqMyAmHf/D7TY
ReS6Oe9w8LgvX4tCaIL2Ik2wWK6Ubp6PXaXNSPquZjP4zhyXGEyWmsHq9/FW9ATk
TlBOu2GmzKTgO9ief5DL0P1vuE2dDgaSj9bW/LsNvdCysQkcZKH4ocjp4NsLdeOj
qLvzXy0uigcNTM+QbEKDSMJl/KMCeyT9O7fXvsbpv74ajefz/DcDKKeGzXF/NSXg
lNUC+F8bU/XLiUkGi/yDix4+kVnSeujcsNUgqGuBdawFmerB4L4KrBj1MEaP5nOw
feY0V2jysUkr2m6PtubVgxJFF8AV0FpBA8bjzChoz54DuMLu8Xq7BZjlFRNrMjkr
RwtGyCmyHE9QyHyeAGqhYil2Pkw8OmncIY5RjglnOyrPp9lMjG0ZtHQR628kvoQP
AmmsxZHU3PYCzQoAZvsc8UZICXH4In0KyezE6iHn6OBA7v5c61ViBnJmg79pRyKX
BNWxtfBFrnRNvPop0iZjZYtDEN4H1Uc+9tXcU4ljtgB7a1GpYr8OcZ1X7EsfhQRb
CUhRL8cTmrU5+m+1xcV7QsECbl611PGeyW+c99kN2fK2wAlSxjpd6XTY84WQxIIE
HHQVqooqP+cnndvakaNqHkFCtzepAoSu3gMwOIl2ZliWbqfu5skZMgC9fvVgemSc
n1lmdvsSTc0IfcrvtZszbytgg5iM4SEMfZhEdeJpu56Ag4Zv7GvJdapZpQv6ugXR
JPhC77/Xbgfc1nvhFK7FVwPwHl6q4pXQDMaLvNWSxkfUECvO/4vDSXe1SPoLW+gb
EK/udCjcRyaHADin8r1fdSaN+V2lP72Jbgx5yALotyYOz9As9p5l9oSTurE=
=GOQf
-----END PGP MESSAGE-----
```


## Decrypting a file

```

GPG_KEY_ID=CodyLane ./gpg-sae decrypt encrypt_this_file.asc

┌────────────────────────────────────────────────────────────────┐
│ Please enter the passphrase to unlock the OpenPGP secret key:  │
│ "CodyLane <xxxxxxxxx@example.com>"                             │
│ 4096-bit RSA key, ID 123CB55F1237F123                          │
│ created 2020-02-22 (main key ID xxxxxxxxxxxxxxxx).             │
│                                                                │
│ Passphrase: *************************************___________   │
│                                                                │
│         <OK>                                    <Cancel>       │
└────────────────────────────────────────────────────────────────┘

```

- Next we validate the file is no longer encrypted

#### `ls -l encrypt_this_file*`

```
-rw-r--r-- 1 x y 53   Feb 20 00:00 encrypt_this_file
-rw-r--r-- 1 x y 1747 Feb 20 00:00 encrypt_this_file.asc
```

- And we can finally validate our original contents

#### `cat encrypt_this_file`

```
this is my special file that I would like to encrypt
```

# Author

- Cody Lane 2020
