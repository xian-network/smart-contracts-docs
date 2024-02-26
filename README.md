# Contracting

Contracting is a subset of Python designed for writing, testing, and deploying smart contracts with ease and efficiency. Our goal is to make blockchain development as intuitive and accessible as possible, leveraging the simplicity of Python to offer a seamless smart contract development experience.

## Table of Contents

- [Contracting](#contracting)
  - [Table of Contents](#table-of-contents)
  - [Introduction](#introduction)
  - [Features](#features)
  - [Getting Started](#getting-started)
    - [Reference Contract](#reference-contract)
  - [Documentation](#documentation)
  - [Contributing](#contributing)

## Introduction

Contracting simplifies the process of creating, testing, and deploying smart contracts by providing a Pythonic interface to the blockchain. Whether you're a beginner in blockchain technology or an experienced developer looking to streamline your smart contract development workflow, Contracting is designed to enhance your productivity and make blockchain development accessible to a wider audience.

## Features

- **Pythonic Syntax**: Write smart contracts with the simplicity and elegance of Python.
- **Integrated Testing Tools**: Test your contracts with built-in frameworks that simulate blockchain environments.
- **Easy Deployment**: Deploy your contracts to the blockchain with the wallet.
- **Modular Design**: Reuse and share contracts as modules to build complex decentralized applications.

## Getting Started

### Reference Contract

```python
random.seed()

simple_var = Variable() # Variable is a way to define a state variable in the contract
storage = Hash(default_value=0) # Hash is a way to define a key-value store in the contract
submission_time = Variable()
submission_block_num = Variable()
submission_block_hash = Variable()
random_number = Variable()

currency_balances = ForeignHash(foreign_contract='currency', foreign_name='balances') # ForeignHash is a way to get a read-only view of a hash from another contract
foundation_owner = ForeignVariable(foreign_contract='foundation', foreign_name='owner') # ForeignVariable is a way to get a read-only view of a variable from another contract

@construct # The construct decorator is used to define initialization logic for the contract
def seed():
    # Initialize the contract with a variable
    simple_var.set(0)
    submission_time.set(now) # now is a built-in function that returns the current datetime
    random_number.set(random.randint(0, 100))
    submission_block_num.set(block_num) # block_num is a built-in function that returns the current block number
    submission_block_hash.set(block_hash) # block_hash is a built-in function that returns the current block hash

def private_function(): # This function is private and cannot be called from outside the contract
    # This function is private and cannot be called from outside the contract
    return "This is a private function"

@export # The export decorator is used to define functions that can be called from outside the contract
def call_private_function():
    # Call the private function
    return private_function()

@export
def public_function():
    # This function is public and can be called from outside the contract
    return "This is a public function"

@export
def increment():
    # Increment the variable by 1
    simple_var.set(simple_var.get() + 1)

@export
def decrement():
    # Decrement the variable by 1
    simple_var.set(simple_var.get() - 1)

@export
def set_storage_pair(key: str, value: int):
    # Set a key-value pair in the storage
    storage[key] = value

@export
def get_storage_pair(key: str):
    # Get the value of a key in the storage
    return storage[key]

@export
def set_nested_storage_pair(key: str, nested_key: str, value: int):
    # Set a nested key-value pair in the storage
    storage[key, nested_key] = value

@export
def get_nested_storage_pair(key: str, nested_key: str):
    # Get the value of a nested key in the storage
    return storage[key, nested_key]

@export
def interact_with_other_contract(contract: str, args: dict):
    c = importlib.import_module(contract) # Import another contract dynamically

    forced_interface = [
        importlib.Func('do_something', args=('amount', 'to')), # Func is a way to enforce the existence of a function with specific arguments
        importlib.Var('balances', Hash) # Var is a way to enforce the existence of a variable with a specific type
    ] 

    assert importlib.enforce_interface(c, forced_interface) # Enforce the interface of the other contract

    # Interact with another contract
    c.do_something(**args)

@export
def get_contract_name():
    return ctx.this

@export
def who_am_i():
    return ctx.caller # The actual caller that called this function. Could be a contract or an account

@export
def get_top_level_signer():
    return ctx.signer # First signer in the call chain (the original signer). This is the account that initiated the transaction even if the transaction was forwarded by another contract
```

## Documentation

Upcoming.

## Contributing

We welcome contributions from the community. If you have any ideas, suggestions, or bug reports, please open an issue or submit a pull request.
