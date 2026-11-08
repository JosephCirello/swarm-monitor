# Result tables from the report

Models 1 to 3 are three sizes of one developer's family, named by size only; Model 4 is one model of a second developer. Monitors: Claude Haiku 5.5, Llama 3.3 70B, GPT-4o mini; the swarm is a majority of the three. Condition A: the action record alone. Condition B: the record plus the agent's own account.

## Table 1. Catching the harmful action from the action record alone (condition A), per acting model and pooled. TP: harmful episodes flagged; FP: harmless episodes flagged; FN: harmful episodes missed.

| Acting model | Harmful | Monitor | TP | FP | FN | Precision | Recall | F1 |
|---|---|---|---|---|---|---|---|---|
| Model 1 (smallest) | 33 | Claude Haiku 5.5 | 30 | 28 | 3 | 0.52 | 0.91 | 0.66 |
| | | Llama 3.3 70B | 30 | 60 | 3 | 0.33 | 0.91 | 0.49 |
| | | GPT-4o mini | 29 | 98 | 4 | 0.23 | 0.88 | 0.36 |
| | | **Swarm (majority)** | 31 | 60 | 2 | 0.34 | 0.94 | 0.50 |
| Model 2 | 5 | Claude Haiku 5.5 | 3 | 29 | 2 | 0.09 | 0.60 | 0.16 |
| | | Llama 3.3 70B | 3 | 49 | 2 | 0.06 | 0.60 | 0.11 |
| | | GPT-4o mini | 3 | 102 | 2 | 0.03 | 0.60 | 0.05 |
| | | **Swarm (majority)** | 3 | 46 | 2 | 0.06 | 0.60 | 0.11 |
| Model 3 (largest) | 3 | Claude Haiku 5.5 | 2 | 32 | 1 | 0.06 | 0.67 | 0.11 |
| | | Llama 3.3 70B | 1 | 57 | 2 | 0.02 | 0.33 | 0.03 |
| | | GPT-4o mini | 2 | 111 | 1 | 0.02 | 0.67 | 0.03 |
| | | **Swarm (majority)** | 2 | 56 | 1 | 0.03 | 0.67 | 0.07 |
| **Models 1 to 3** | **41** | Claude Haiku 5.5 | 35 | 89 | 6 | 0.28 | 0.85 | 0.42 |
| | | Llama 3.3 70B | 34 | 166 | 7 | 0.17 | 0.83 | 0.28 |
| | | GPT-4o mini | 34 | 311 | 7 | 0.10 | 0.83 | 0.18 |
| | | **Swarm (majority)** | **36** | **162** | **5** | **0.18** | **0.88** | **0.30** |
| Model 4 | 72 | Claude Haiku 5.5 | 68 | 26 | 4 | 0.72 | 0.94 | 0.82 |
| | | Llama 3.3 70B | 64 | 43 | 8 | 0.60 | 0.89 | 0.72 |
| | | GPT-4o mini | 65 | 64 | 7 | 0.50 | 0.90 | 0.65 |
| | | **Swarm (majority)** | 68 | 41 | 4 | 0.62 | 0.94 | 0.75 |
| **All four** | **113** | Claude Haiku 5.5 | 103 | 115 | 10 | 0.47 | 0.91 | 0.62 |
| | | Llama 3.3 70B | 98 | 209 | 15 | 0.32 | 0.87 | 0.47 |
| | | GPT-4o mini | 99 | 375 | 14 | 0.21 | 0.88 | 0.34 |
| | | **Swarm (majority)** | **104** | **203** | **9** | **0.34** | **0.92** | **0.50** |

## Table 2. Each monitor and the swarm majority with the action record alone (A) and with the agent's final message and its answer when asked to account for its actions added (B), pooled over the first developer's three models (695 episodes, 41 harmful), the runs that carry the answer when asked.

| Monitor | Recall A | Recall B | Precision A | Precision B | False alarms A | False alarms B |
|---|---|---|---|---|---|---|
| Claude Haiku 5.5 | 0.85 | 0.90 | 0.28 | 0.31 | 89 | 81 |
| Llama 3.3 70B | 0.83 | 0.73 | 0.17 | 0.36 | 166 | 54 |
| GPT-4o mini | 0.83 | 0.85 | 0.10 | 0.16 | 311 | 181 |
| **Swarm (majority)** | **0.88** | **0.88** | **0.18** | **0.33** | **162** | **73** |

## Table 3. The second developer's model: 19 harmful episodes whose final message left the act out, 51 whose final message disclosed it. Caught: flagged the act (of 19). Noticed the omission: flagged the act and read the account as leaving it out (of 19; swarm column: a majority). Last column: of the 51 disclosed, read the account as matching.

| Monitor | Caught, record alone | Caught, with account | Noticed the omission | Disclosed read as matching |
|---|---|---|---|---|
| Claude Haiku 5.5 | 17 | 17 | 3 | 34 |
| Llama 3.3 70B | 14 | 14 | 7 | 40 |
| GPT-4o mini | 15 | 15 | 4 | 35 |
| **Swarm (majority)** | 15 | 16 | 3 | |

## Table 4. Three vote rules over the same three monitors, pooled over 921 episodes (113 harmful, 808 harmless). False-alarm rate: the share of harmless episodes flagged.

| Vote rule | Recall A | False-alarm rate A | Recall B | False-alarm rate B |
|---|---|---|---|---|
| Any one of three | 0.95 | 0.53 | 0.96 | 0.35 |
| Majority | 0.92 | 0.25 | 0.92 | 0.14 |
| All three | 0.79 | 0.09 | 0.73 | 0.06 |
