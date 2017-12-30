# parity-poa-tutorial
A complete set of files produced in the Parity PoA chain tutorial.

# Step by Step 
Follow the [tutorial on GitHub](https://github.com/paritytech/parity/wiki/Demo-PoA-tutorial). Below is a simplification, with some tweaking of the files to make things work. You can run these steps first, and then go back to the tutorial to understand in greater details.

The following assumes you're running on Linux Ubuntu with Parity installed. You can do this on the same machine (the configuration files take care of picking different ports).

## 1. Run the chain to create the accounts on both nodes
Type these lines in two separate terminals:  
`$ parity --config node0.starthere`  
`$ parity --config node1.starthere`  

Open another terminal, running from this directory (where this README file is located), and execute the following scripts:  
`$ ./create_first_authority_address_on_node0.sh`  
`$ ./create_second_authority_address_on_node1.sh`  
`$ ./create_user__address_on_node0.sh`  

Kill the two parity processes (in the other consoles).

## 2. Run the chain with full mining configuration
Now that the accounts are created, let's promote them as validator authorities. Type these lines in two separate terminals:  
`$ parity --config node0.toml`  
`$ parity --config node1.toml`  

## 3. Setup the Parity Web UI
Open two different windows or tabs in your browser for node 0 (at http://localhost:8180) and node 1 (at http://localhost:8181).

Restore the accounts (in the accounts tab):  
* node 0: restore accounts `node0` (password = node0), and user (password = user)  
* node 1: restore account `node1` (password = node1)  

## 3. Connect the two nodes with each other
Check the console were you started node 0, and look for the Public Node URL. It should ressemble something like this: `enode://<long hash>@<IP Address>:<Port Number>`

Go to the Status tab (the leftmost tab) in the Web UI for node 1, and look for the Network Peers section. Click on `ADD RESERVED`, and copy the URL (including enode://). You should see an entry, and a corresponding one in the Web UI for the other node. Voilà! 

Check the console output and the Web UI. Both should acknowledged another peer (1/25 Peers instead of 0/25 Peers).

## 4. Send transactions
Run the following scripts and watch the balance for each account in the Web UIs.  
`$ send_from_user_to_node0_account.sh`  
`$ send_from_user_to_node1_account.sh`  

You can also try in a separate console, where you can read the JSON-formatted response.  
`$check_balance_in_node0_account.sh`  
`$check_balance_in_node1_account.sh`  

## 5. Add nodes to the network
Run parity with the right chain specification and let other nodes know (by adding them by enode URL). You just need the demo-spec.json file to get started.  
`$ parity --chain demo-spec.json`

