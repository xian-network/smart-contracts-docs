## Crypto Standard Library

The `crypto` module uses the `PyNaCl` library under the hood, employing the `Ed25519` signature scheme. The module consists of the following functions

### verify_signature

It checks if the signature is valid for the given message and verification key. The result (True or False) is then returned. This can be used to ensure data integrity and authenticity in transactions within the smart contract environment.

How to use it in a contract:

```python
@export
def verify_signature(vk: str, msg: str, signature: str):
    # Check if the signature is valid for the given message and verification key
    is_valid = crypto.verify(vk, msg, signature)
    
    # Return the result of the verification
    return is_valid
```

### key_is_valid

It checks if the provided key (address) is valid or not. The result (True or False) is then returned.

How to use it in a contract:

```python
@export
def verify_address(address: str):
    # Check if the given address is a valid Ed25519 key
    is_valid = key_is_valid(address)
    
    # Return the result of the verification
    return is_valid
```