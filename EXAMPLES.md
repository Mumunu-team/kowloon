# Examples

Four worked spec items, one per kind of project. They explain; they carry no rules. Each shows the item, its check as a trace-map line, and its negative control.

## Hardware (RTL)

```
SPEC-FIFO-003 | behaviour | wr_ready is never high while the FIFO is full
checked-by: check | under: SPEC-FIFO-004 (a single write clock)
SPEC-FIFO-003@1   check   formal:fifo_top.a_no_overflow=proved
SPEC-FIFO-004@1   check   formal:fifo_top.c_full_reached=covered
```

- **Negative control:** a variant with the full comparison off by one. The same label must return a counterexample.
- **Witness:** the cover runs under the same assumptions as the property, and shows the FIFO can fill.

## Agent orchestration

```
SPEC-ROUTE-002 | budget | A refund request above 100 EUR is handed to a human in at least 98% of 200 runs
checked-by: measurement | under: SPEC-ROUTE-003 (the pinned model)
SPEC-ROUTE-002@1   check   evals:refund_escalation>=0.98
```

- **Check:** seeds fixed, the verdict read from the tool-call log and not from a model acting as judge.
- **Negative control:** the same evaluation with the escalation paragraph removed from the router's instructions. It must score below 0.98 over all 200 runs.

## Software

```
SPEC-EXP-004 | behaviour | Export never leaves a partial file: on any error the destination is unchanged
checked-by: check
SPEC-EXP-004@1   check   pytest:tests/test_export.py::test_atomic_on_error=pass
```

- **Check:** a property test that fails each write in turn.
- **Negative control:** a mutation that removes the rename from the temporary file. The test must fail.

## Robotics

```
SPEC-STOP-001 | behaviour | With any lidar return inside 0.5 m, commanded velocity is zero within 100 ms
checked-by: check, measurement | under: SPEC-STOP-002 (scans arrive at 10 Hz or more)
SPEC-STOP-001@1   check   sim:estop_obstacle_sweep=pass
SPEC-STOP-001@1   check   hil:estop_latency<=100ms
```

- **Checks:** a simulation sweep the gate can run, and a hardware-in-the-loop latency kept as a recorded result with its tool version, content hash and operator.
- **Negative control:** a variant with the monitor threshold at 0 m, in simulation only. The sweep must fail.
- **Not covered:** that the simulator matches the robot. That stays an assumption.
