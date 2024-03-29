# Chapter 07: Transactions

## Section 2 Weak Isolation Level

### Read Committed

The most basic level of transaction isolation, which makes 2 guarantees

1. When reading from the database, one will only see data that has been committed (no dirty reads)
2. When writing to the database, you will only overwrite data that has been committed (no dirty writes)

#### No dirty reads

That one transaction can see the uncommitted data in another transaction is called a _dirty read_.

#### No dirty writes

That an ealier write, which is part of a transaction, has not yet commited, but the latter write overwrites an uncommitted value, is called a _dirty write_.

#### Implementing read committed

TODO - to prevent dirty reads

TODO - to prevent dirty writes

### Snapshot Isolation and Repeatable Read

Snapshot isolation is that each transaction reads from a consistent snapshot of the database --- that is, the transaction sees all the data that was committed in the database at the start of the transaction. Even if the data is subsequently changed by another transaction, each transaction sees only the old data from that particular point in time.

#### Implementing snapshot isolation

A key principle of snapshot isolation is that _readers never block writers, and writers never block readers_.

#### Visibility rules for observing a consistent snapshot

TODO - 4 rules

#### Indices nd snapshot isolation

TODO

#### Repeatable read and naming confusion

Snapshot isolation is a useful isolation level, especially for read-only transactions.

### Preventing Lost Updates

TODO

#### Atomic write operations

- Atomic operations are usually implemented by taking an exclusive lock on the object when it is read so that no other transaction can read it until the update has been applied. This technique is sometimes known as _cursor stability_.
- Another option is to simply force all atomic operations to be executed on a single thread.

#### Explicit locking

TODO

#### Automatically detecting lost updates

TODO

#### Compare-and-set

It allows a write to happen **only** if the value has not been concurrently changed by someone else.

#### Conflict resolution and replication

TODO

### Write Skew and Phantoms

TODO

#### Characterizing write skew

TODO

#### More examples of write skew

TODO

#### Phantoms causing write skew

The effect, where a write in one transaction changes the result of a search query in another transaction, is called a _phantom_.

Snapshot isolation avoids phantoms in read-only queries, but in read-write transactions, phantoms can lead to particularly tricky cases of write skew.

TODO

#### Materializing conflicts

It takes a phantom and turns it into a lock conflict on a concrete set of rows that exist in the database.

TODO
