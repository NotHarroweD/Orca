# SPEC-003: Stack limits

## Why
Items should stack up to a maximum so inventories stay manageable.

## Allowed files
- src/inventory.py
- tests/test_stack_limits.py

## Task
In `Inventory.add(item, count)`: an item type stacks up to MAX_STACK.
If adding would exceed it, fill the existing stack to the limit and put the remainder in a new stack.
If no slot is free for the remainder, raise InventoryFullError and leave the inventory exactly as it was.

## Facts
- MAX_STACK = 99 (decisions.md)
- `Inventory` has `slots` (an int, the capacity) and `stacks` (a list of (item, count) pairs).
- `InventoryFullError` already exists in src/errors.py. Import it; do not redefine it.

## Tests (write first; they must fail before you implement)
- adding 50 to a stack of 60 gives stacks of 99 and 11
  - break: change the limit to 100; this test must fail
- adding when all slots are full raises InventoryFullError AND `stacks` is unchanged afterwards
  - break: remove the rollback; this test must fail

## Checks
./check

## Commit
feat(inventory): add stack limits

## Out of scope
Weight limits, saving, any refactoring.
