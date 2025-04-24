# 📘 Control Flow Analysis and Loop Optimization

This project implements several foundational compiler analysis techniques on a list of statements to understand control flow, data dependencies, and identify optimization opportunities like loop invariants.

## 🔧 Technologies Used

- Python
- NetworkX (for visualizing flow graphs)
- Matplotlib (for rendering the graph)

---

## 🚦 Steps of Analysis

### 1️⃣ Finding Leaders

**Function:** `find_leaders(statements)`

Leaders mark the beginning of basic blocks. A statement is considered a leader if:
- It is the first statement.
- It is the target of a `goto`.
- It immediately follows an `if` statement with a `goto`.

---

### 2️⃣ Forming Basic Blocks

**Function:** `form_basic_blocks(statements, leaders)`

Using the identified leaders, the code groups statements into **basic blocks**. A basic block is a sequence of statements with:
- A single entry point (the leader)
- A single exit point (typically a jump or the start of another block)

---

### 3️⃣ Constructing the Program Flow Graph (CFG)

**Function:** `construct_flow_graph(basic_blocks, stmt_to_block)`

Builds a directed graph where:
- Nodes are basic blocks.
- Edges represent control flow between blocks, determined by sequential execution and `goto` targets.

Visualization is done via `visualize_flow_graph()`.

---

### 4️⃣ IN/OUT Set Calculation (Data Flow Analysis)

**Functions:**
- `compute_gen_kill(basic_blocks)`
- `compute_predecessors(flow_graph)`

Defines:
- `GEN[B]`: Definitions generated in a block.
- `KILL[B]`: Definitions that a block invalidates.

Then uses these to iteratively compute:
- `IN[B]`: Definitions reaching the beginning of a block.
- `OUT[B]`: Definitions reaching the end of a block.

---

### 5️⃣ Use-Definition Chains (UD-Chains)

**Functions:**
- `calculate_ud_chains(statements, IN)`
- `generate_mappings(statements, basic_blocks)`

Creates UD-Chains by mapping:
- Each variable to the set of statements where it’s used.
- Back to the definitions that can reach these uses.

---

### 6️⃣ Loop Invariant Code Detection

**Functions:**
- `detect_loops(flow_graph, dominators)`
- `get_loop_statements(loops, stmt_to_block)`
- `identify_loop_invariants(ud_chains, loop_statements)`

Finds:
- **Natural loops** using back edges in the CFG.
- **Loop-invariant code** by analyzing whether a variable is redefined inside the loop.

---

## 📈 Output

- **Leaders**
- **Basic Blocks**
- **Flow Graph (visualized)**
- **Dominators**
- **Natural Loops**
- **GEN & KILL Sets**
- **IN & OUT Sets**
- **UD-Chains**
- **Loop-Invariant Variables**

---

## ✅ Example Use Case

Given a simple loop in pseudo-code, this tool shows:
- Control dependencies
- Data flow
- Optimization potential (e.g., moving loop-invariant code out of the loop)

Perfect for understanding compiler backend logic or writing optimization passes.

---
