# Deployment Automation

This repository contains Ansible and Terraform scripts to automate deployment of new networks
resembling "POA Network".

Namely, the following operations are performed:
- A random account is generated for Master of Ceremony (MoC)

- The bytecode of the Network Consensus Contract gets compiled

- Based on the prior data, the genesis JSON file gets generated

- A netstat node is started

- Several (configurable number) boot nodes are started, `boot nodes.txt` is exchanged between them.

- Additionally, some more boot nodes can be started behind a Gateway, forming a publicly
accessible RPC endpoint for the network. This endpoint is available over `http`, but the
user may later assign it a DNS name, generate valid SSL certificates and upload them to the
Gateway config, turning this endpoint to `https`.

- The explorer node is started.

- The MoC node is started.

- The ceremony is performed on the MoC node, i.e. other consensus contracts are deployed to
the network.

- Several (configurable number) initial keys are generated.

- A subset (or all) of the initial keys are converted into (mining + voting + payout) keys.

- For a subset (or for all) of converted keys, validator nodes are started.

- Simple tests can be run against the network: (1) check that txs are getting mined (2) check that
all validators mine blocks (only makes sense if validator nodes were started for all mining keys).

- Artifacts (`spec.json`, `boot nodes.txt`, `contracts.json`, ...) are stored on the MoC node.

- A `hosts` file is generated on the user's machine containing IP addresses of all nodes and
their respective roles.

Most of the work is done by `ansible`, but to bring up the infrastructure, ansible uses `terraform`.

## Usage

Currently, only deployment to Azure is supported:
[Azure deployment README](azure/README.md)

