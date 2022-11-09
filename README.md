# Access BSC TX Pool easy & fast


## 1. Signup at Quicknode

### https://bit.ly/free-quicknode-signup


## 2. Create BSC Endpoint

## 3. Install Python with Web3 (if not already done)

```
pip3 install Web3
```


## 4. This is the code for TX Pool Access

```python
#imports
from datetime import datetime
from web3 import Web3
from web3 import Web3, IPCProvider, exceptions
from web3.middleware import geth_poa_middleware


#you need a quicknode endpoint, not working with public endpoints
#
# https://bit.ly/free-quicknode-signup
#


#ENTER HERE YOUR QUICKNODE ENDPONT
quick_node_http_endpoint = "<insert your quicknode endpoint here"


#connect to node
w3 = Web3(Web3.HTTPProvider(quick_node_http_endpoint))
w3.middleware_onion.inject(geth_poa_middleware, layer=0)


#access TX Pool and loop
new_transaction_filter = w3.eth.filter("pending")
while True:
    try:
        evt = new_transaction_filter.get_new_entries()
        if len(evt) > 0:
            for args in evt:
                try:
                    tx = w3.eth.getTransaction(w3.toHex(args))
                    #tx contains now the transaction that is going to be mined
                    print (f'{str(datetime.now())} - {tx["hash"].hex()}')
                except KeyboardInterrupt:
                    quit()
                except exceptions.TransactionNotFound:
                    #tx not found
                    print (f'tx not found!')
                except Exception as e:
                    print(f"Error: {e}")
    except KeyboardInterrupt:
        quit()
    except:
        pass
```


## 5. if this Code makes you rich you can support me with a little bit BNB/ETH/...

This is my wallet: 0x1D415B974b9d8F831c999160c7b995d420CFabA6

