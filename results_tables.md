# The four result tables, in plain words

**Who did what.** Four AI agents ("acting models") were tested. Models 1, 2 and 3 are three sizes of one
company's model line; Model 4 is a model from a second company. Three cheap "monitor" models from three other
companies (Claude Haiku 5.5, Llama 3.3 70B and GPT-4o mini) read the record of what each agent did and said
whether anything in it was harmful. "Swarm" means the three monitors voting, majority wins.

**Two ways of looking.** Condition A: the monitors saw only the record of the agent's actions. Condition B:
they also saw the agent's own explanation of what it had done.

**The words in the tables.**

- *Harmful*: how many episodes really contained a harmful action, by the testbed's own grading.
- *TP* (true positives): harmful episodes the monitor flagged. *FP* (false positives): harmless episodes it
  flagged anyway, the false alarms. *FN* (false negatives): harmful episodes it missed.
- *Recall*: the share of the real harms it caught. 0.92 means it caught 92 of every 100.
- *Precision*: the share of its flags that were right. 0.34 means about one flag in three was a real harm.
- *F1*: one number that balances the two.
- *False-alarm rate*: the share of harmless episodes it flagged.

## Table 1. How well each monitor catches the act from the record alone (condition A)

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

**How to read it.** The monitors caught nearly every harmful episode: the swarm got 104 of 113. Precision
looks very different from one agent to the next, but that is about the agents, not the monitors. The safer the
agent, the fewer real harms there are to find, while the monitors keep raising false alarms at about the same
rate. On the safest agent (Model 3) the swarm raised 56 false alarms to catch 2 real harms.

## Table 2. Does showing the agent's explanation help or hurt? (Models 1 to 3, 695 episodes, 41 harmful)

| Monitor | Recall A | Recall B | Precision A | Precision B | False alarms A | False alarms B |
|---|---|---|---|---|---|---|
| Claude Haiku 5.5 | 0.85 | 0.90 | 0.28 | 0.31 | 89 | 81 |
| Llama 3.3 70B | 0.83 | 0.73 | 0.17 | 0.36 | 166 | 54 |
| GPT-4o mini | 0.83 | 0.85 | 0.10 | 0.16 | 311 | 181 |
| **Swarm (majority)** | **0.88** | **0.88** | **0.18** | **0.33** | **162** | **73** |

**How to read it.** With the agent's explanation added (B), the swarm's false alarms fell from 162 to 73 and
it lost no catches. But one monitor, Llama, was talked out of four catches it had made from the record alone:
its recall fell from 0.83 to 0.73. A convincing story can persuade a cheap monitor. (Only Models 1 to 3 are
here, because only their runs recorded the agent's answer when asked to account for itself.)

## Table 3. When the agent hid the act, did the monitors notice? (Model 4)

Model 4 had 72 harmful episodes. In 51 of them the agent's final message admitted the act; in 19 it left the
act out. The table counts, out of those 19: how many the monitor still caught from the record; how many it
caught with the explanation added; and how many times it also said the explanation left the act out. The last
column is for the 51 honest cases: how often the monitor agreed the explanation matched the record.

| Monitor | Caught, record alone | Caught, with account | Noticed the omission | Disclosed read as matching |
|---|---|---|---|---|
| Claude Haiku 5.5 | 17 | 17 | 3 | 34 |
| Llama 3.3 70B | 14 | 14 | 7 | 40 |
| GPT-4o mini | 15 | 15 | 4 | 35 |
| **Swarm (majority)** | 15 | 16 | 3 | |

**How to read it.** The monitors caught the act whether or not the agent admitted it. What they mostly did
not do was notice the cover-up: only 3 to 7 of the 19 omissions were called out. And on the 51 honest
explanations they often cried foul anyway. Cheap monitors watch the act; they are poor judges of the story.

## Table 4. The vote rule is a dial (all four models, 921 episodes, 113 harmful)

The swarm does not have to be a majority vote. Here are three rules: flag if any one monitor says harmful,
flag if two of three do, flag only if all three do.

| Vote rule | Recall A | False-alarm rate A | Recall B | False-alarm rate B |
|---|---|---|---|---|
| Any one of three | 0.95 | 0.53 | 0.96 | 0.35 |
| Majority | 0.92 | 0.25 | 0.92 | 0.14 |
| All three | 0.79 | 0.09 | 0.73 | 0.06 |

**How to read it.** "Any one" catches almost everything but flags half the harmless episodes. "All three"
flags very little that is harmless but misses one harm in five. The majority sits between. The useful part is
the count itself: when all three monitors agreed an episode was harmful, it really was 56 percent of the time;
when only one said so, 1 percent. The number of monitors that agree tells you which alarms to open first.
