# Contracts

**WIP**

Contracts are similar to Traits in Rust, or interfaces in object-oriented languages.

## Defining contracts

Every contract has the implicit generic type `self` as placeholder for any type that may comply to the contract.

A contract is defined like a struct type definition, and may add default implementations if applicable.

```
{#contract From<T> := (
  from: (other: T) self
)/}
```

## Complying to contracts

Any type may comply to a contract, by implementing all macros defined in the contract. Types and memorables defined in a contract are automatically added to the complying type.

```
{#comply int to From<nat>}
  {#macro from (other: nat) int}
    {$other}
  {/end}
{/end}
```
