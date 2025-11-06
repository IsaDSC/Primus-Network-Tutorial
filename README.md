## **Overview**

zkTLS verifies TLS data authenticity while preserving privacy, without modifying servers. It enables secure use of Web2 personal data for efficient cross-platform flow.

Primus provides unified SDKs for both **Dapp** and **Backend** integrations, allowing you to prove any HTTPS data through zkTLS protocols.

## zkTLS Mode

zkTLS supports two algorithm modes, each with different trade-offs between security and performance.

### **MPC Mode**

The attestor and client jointly execute secure multi-party computation to generate TLS session materials, preventing the client from modifying data before the attestor returns its key share.

Primus' MPC mode uses [QuickSilver](https://eprint.iacr.org/2021/076), an efficient interactive zero-knowledge proof system. QuickSilver significantly reduces computational and communication overhead. See our [whitepaper](https://eprint.iacr.org/2023/964) for details.

💡 **Use MPC mode** when integrity against client-side tampering is your highest priority.

### **Proxy Mode**

The attestor intermediates between client and server, forwarding TLS traffic and recording ciphertexts. At session end, the client proves it knows the plaintext messages.

Proxy mode offers better performance by avoiding multi-party computation overhead. However, the attestor must verify it's communicating with the intended server.

Primus' Proxy mode uses the efficient [QuickSilver](https://eprint.iacr.org/2021/076) protocol and proves Key Derivation Functions (KDFs) during TLS establishment—typically inefficient in zk-SNARK alternatives. This eliminates extra padding.

💡 **Use Proxy mode** when performance and throughput are key considerations.

## Before You Begin

Make sure your environment includes:

- **Node.js ≥ 18**
- **npm / yarn**
- Access to a supported blockchain RPC (for onchain verification)
