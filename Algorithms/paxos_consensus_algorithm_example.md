# Paxos by Example #
1. It is a decentralized consensus algorithm.
    1. Distributed consensus algorithms are used to enable set of computers to agree on a single value
        1. Example: `commit` or `rollback` done using two- or three-phase commit
            1. Two-phase commit:
                1. Two-phase Commit (2PC) is a protocol for ensuring that a transaction is either **completed** or **completely rolled back** in a distributed system, ensuring atomicity across **multiple databases** or **participants**. It involves two phases:
                    1. A decision phase: Participants agree to either commit or abort the transaction.
                    2. A confirmation phase: Participants act on the agreed decision.
                2. Example:
                    1. Consider a banking transaction where money is transferred from **one account** to **another**
                        1. The two participants are source and destination accounts respectively
                    2. Phase 1: Decision Phase
                        1. Source account sends a request to destination account to confirm if it is ready to accept the transfer.
                        2. Destination account sends a response back to source account indicating its readiness (or not) to commit the transaction.
                    3. Phase 2: Confirmation Phase
                        1. If destination account is ready, source account sends a commit message, and transfer of money takes place.
                        2. If destination account is not ready, source account sends an abort message, and transaction is rolled back to its original state.
                    4. 2PC ensures that transaction is either completely committed or completely rolled back (preventing inconsistencies)
            2. Three-phase commit:
                1. It is a distributed consensus protocol used to ensure consistency and durability of transactions across multiple nodes in a network.
                2. It has 3 phases:
                    1. Prepare
                    2. Commit
                    3. Acknowledge
                        1. To ensure all nodes agree on the outcome of a transaction before it is permanently committed to a database
                3. Example:
                    1. Phase 1 (Prepare):
                        1. Initiating node (e.g. account holder's branch) sends a request to all other nodes to prepare for the transaction.
                        2. Each node checks if it has sufficient funds and, if so, sends a "ready" signal back to the initiating node.
                    2. Phase 2 (Commit):
                        1. If all nodes have send the "ready" signal, initiating ndoe sends a commit request to all nodes to make the transaction permanent.
                    3. Phase 3 (Acknowledge):
                        1. Each node acknowledges receipt of the commit request and makes the transaction permanent in its own database.
                        2. If any node fails to acknowledge, the transaction is rolled back and the initiating node is notified.
                    4. The process ensures that the transaction is **consistent** and **durable** across bank's network and that all nodes agree on the outcome of the transactions before it is committed.
## General Approach ##
## Paxos By Example ##
## References ##