# Installation for Testing

1. Python 3.11.7
    * https://www.python.org/downloads/release/python-3117/
2. Contracting
    * Clone the repository from https://github.com/xian-network/contracting
    * Inside do pip install -e .

## Testing the Installation
Open the Python 3.11.7 REPL, usually by running `python3` in a command terminal. Type the following commands.
```python
In [1]: from contracting.client import ContractingClient
In [2]: client = ContractingClient()
In [3]: client.get_contracts()
Out[3]: ['submission'] 
```
If your output matches, you've successfully installed Contracting. Welcome to the most advance smart contacting system on the planet!