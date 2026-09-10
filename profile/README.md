<p align="center">
  <img "zk-vote.png" alt="ZKVote" width="100%" />
</p>

# ZKVote

**Anonymous DAO Voting on Stellar Soroban**

Privacy-preserving governance using **zero-knowledge proofs, BN254, and Poseidon** on Stellar Protocol 25.

[**GitHub**](https://github.com/ZK-VOTE/ZK-VOTE)

---

## What we build

ZKVote enables DAOs to conduct **anonymous, verifiable voting on-chain**.

Members prove DAO eligibility with a zero-knowledge proof without revealing their identity.

- Permissionless DAO creation
- Soulbound membership
- Poseidon Merkle trees
- Groth16 proof verification
- Anonymous voting
- Relayer-based transaction submission

> **Prove membership. Keep identity private.**

---

## How it works

```text
DAO
 ↓
Membership SBT
 ↓
Identity Commitment
 ↓
Poseidon Merkle Tree
 ↓
Proposal
 ↓
Groth16 Proof
 ↓
On-chain Verification
 ↓
Anonymous Vote
```

---

## Architecture

```text
DAORegistry
     ↓
MembershipSBT
     ↓
MembershipTree
     ↓
Voting
     ↓
Comments
```

Contracts communicate through on-chain admin and membership verification.

---

## Zero-Knowledge Layer

The voting circuit proves:

- Identity commitment
- Merkle membership
- Unique nullifier
- Valid vote choice

**Private inputs:** secret, salt, commitment, Merkle path

**Public inputs:** root, nullifier, DAO ID, proposal ID, vote choice

**Merkle depth:** 18 levels (~262K members per DAO).

---

## Groth16 Verification

ZKVote performs native **BN254 pairing verification** through Stellar Protocol 25 host functions.

```rust
env.crypto()
    .bn254()
    .pairing_check(g1_vec, g2_vec)
```



---

## Contracts

| Contract | Purpose |
| :--- | :--- |
| `dao-registry` | DAO creation & administration |
| `membership-sbt` | Non-transferable membership |
| `membership-tree` | Poseidon Merkle commitments |
| `voting` | Proposals & ZK verification |
| `comments` | Anonymous ZK comments |
| `zkvote-groth16` | BN254 Groth16 verification |

---

## Stack

**Stellar Soroban · Rust · Circom · SnarkJS · Groth16 · BN254 · Poseidon · React · Vite · TailwindCSS · Node.js**

---

## Testing

**391 tests + 6 stress tests** covering contracts, integration, backend, frontend, and circuits.

```bash
cargo test --workspace

./scripts/test/poseidon-kat.sh
./scripts/test/e2e-zkproof.sh
```

---

## Security

ZKVote includes:

- Unique vote nullifiers
- BN254 point validation
- Field validation
- Protected voter secrets
- Backend rate limiting

Known limitations include public vote choices, append-only membership trees, and DAO-admin control of the verification key.

---

## Quick Start

```bash
cargo build --target wasm32v1-none --release
cargo test --workspace

cd backend && npm install && npm run relayer

cd ../frontend && npm install && npm run dev
```

---

## License

MIT

**ZKVote — anonymous governance, verified on-chain.**
