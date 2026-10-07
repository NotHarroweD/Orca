# Implementer report, attempt 1

```
STATUS: COMPLETE
SUMMARY: Added stack-limit logic to Inventory.add. Overflow fills the existing stack and spills into a new one.
         Raises InventoryFullError when no slot is free.
FILES: src/inventory.py
       tests/test_stack_limits.py
COMMITS: feat(inventory): add stack limits
RED: 2 failed (test_overflow_splits_stack, test_full_inventory_raises)
GREEN: 2 passed
BREAKS:
  | break                     | test that failed          | code restored |
  | MAX_STACK changed to 100  | test_overflow_splits_stack | yes           |
  | rollback removed          | (none; test still passed)  | yes           |
CHECKS: ./check passed (14 tests, lint clean)
DEVIATIONS: none
CONCERNS: none
```

At a glance this looks fine. Look closely at the BREAKS table, though. The second break did not make any test fail,
and the report says so without flagging it as a problem. A reader skimming for STATUS and CHECKS would miss it.
That's why the reviewer doesn't read this report first.
