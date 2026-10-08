# EVM Step-Through

An interactive, browser-based Ethereum Virtual Machine visualiser for **COMP1830 Blockchain for Fintech** (University of Greenwich), Lab 2.

**Live:** https://apogiatzis.github.io/comp1830-evm-step-through/

Students execute real EVM bytecode one instruction at a time and watch the **stack**, **memory**, **storage**, **program counter** and **gas** change. The default program is the exact bytecode printed in the lab sheet: the Solidity compiler's output for

```solidity
contract MyContract {
    uint i = 10 + 2 * 2;
}
```

## Programs

Link straight to a program with `?preset=<name>`:

| Program | Link | What it shows |
|---|---|---|
| Lab contract: deploy | `?preset=deploy` | Free memory pointer, `SSTORE` of 14, runtime code returned by `CODECOPY` + `RETURN` |
| Lab contract: deploy sending 1 wei | `?preset=payable` | The non-payable check (`CALLVALUE … JUMPI … REVERT`) and state being undone |
| Lab contract: not enough gas | `?preset=outofgas` | Out of gas at `SSTORE`; all changes undone and all gas consumed |
| Infinite loop | `?preset=loop` | Gas as the protection against infinite loops |
| Arithmetic at run time | `?preset=arith` | `10 + 2 * 2` computed with `MUL` / `ADD` instead of by the compiler |
| Lab contract: call the deployed contract | `?preset=runtime` | The stored runtime code: a contract with no functions always reverts |

## Notes

A small teaching interpreter that implements only the opcodes these programs use, with current (post-Berlin) gas costs, including memory expansion and cold/warm storage access. For deployments it also shows the full transaction cost (base cost, contract creation, calldata, init-code words and code deposit).

Single static page: `index.html` plus the University of Greenwich brand fonts (Cooper Hewitt and Public Sans, SIL Open Font Licence). [three.js](https://threejs.org) 0.170.0 is loaded from jsDelivr.
