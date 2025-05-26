# ATM System - Verilog FSM Design

This project implements a simple **ATM system** in Verilog using a **Finite State Machine (FSM)**. The system handles card input, PIN verification, withdrawal processing, balance management, and error detection.

---

# Features

* FSM-based ATM controller
* Fixed PIN verification (`1010`)
* Locks the user out after 3 incorrect attempts
* Handles withdrawal requests
* Checks for sufficient balance before approving
* Raises an error signal for wrong PIN or insufficient funds
* Resets back to Idle state on reset

---

### FSM States

The design includes 8 main states:

1. **Idle (0001)** – Initial default state
2. **card\_inserted (0010)** – Card has been inserted
3. **pin\_entry (0011)** – User is entering the PIN
4. **pin\_correct (0100)** – Correct PIN entered
5. **balance\_check (0101)** – Displays current balance
6. **withdraw (0110)** – Handles withdrawal transaction
7. **error\_state (0111)** – Triggered by wrong PIN or low balance
8. **logout (1000)** – Ends session and returns to Idle

---

### Inputs

* `clk` – Clock signal
* `rst` – Reset signal
* `card_input` – Card insertion signal
* `pin_input [3:0]` – 4-bit PIN input
* `amount_input [7:0]` – Amount to withdraw
* `withdrawal_request` – Withdrawal trigger

---

### Outputs

* `balance [7:0]` – Current balance after transaction
* `error_signal` – High if an error occurs
* `current_state [3:0]` – Current state of the FSM

---

### Working

1. When `card_input` is high, the system moves from `Idle` to `card_inserted`.
2. The user enters the 4-bit PIN.
3. If the PIN is correct (`1010`), it proceeds to `pin_correct`.
4. If the PIN is wrong and entered incorrectly 3 times, it moves to `error_state`.
5. On correct PIN, the user can request a withdrawal.
6. If the entered amount is less than or equal to the balance, withdrawal is processed.
7. If the amount is more than the available balance, it raises an `error_signal`.
8. The session ends with the `logout` state and returns to `Idle`.

---

### Balance Logic

* The initial balance is fixed at **100**
* Successful withdrawals deduct from the balance
* Failed attempts (wrong PIN or low funds) do not affect balance

---

### How to Simulate

* Use any Verilog simulator (like ModelSim, Vivado, Icarus Verilog, etc.)
* Provide input waveforms or use a testbench to simulate the module
* Observe `balance`, `error_signal`, and `current_state` outputs


