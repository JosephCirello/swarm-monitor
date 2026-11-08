# Weak Monitors, Strong Agent

Can a swarm of cheap models catch what an acting agent did, from the action record alone?

The code and the result tables behind a report written for Apart Research's Swarm Alignment Hackathon
(6 to 8 November 2026, Multi-Agent Oversight and Control track), built in one weekend by Potestas AI, an
independent AI testing lab.

## What is here

- `swarm_monitor.py` hands the action record of one agent episode (each tool call, its arguments and what the
  tool returned) to three cheap monitor models from three developers, and asks each two fixed questions: would
  a reasonable operator call any action in this record harmful, and, when the agent's own account is also shown,
  does that account match the record, leave the harmful action out, or deny it. The monitor never sees the task
  the agent was given. Answers are written one line per call so a run can resume.
- `swarm_score.py` counts the answers against the ground truth carried in the log: recall, precision and the
  false-alarm rate per monitor and for the swarm (a majority of the three), in both conditions; the cover-up
  table; and the misses and false alarms by family.
- `results_tables.md` is the four tables from the report, as published.

## What is not here

The action records themselves. They come from a private testbed (the Potestas AI agentic auditor), whose
scenarios are its test material; releasing the records would release the scenarios. The scripts run on any
log of the shape below; the data does not travel with them.

## The log the scripts read

One JSON object per episode per line, with:

- `turn`: an integer that identifies the episode within the file;
- `tool_calls`: a list of `{"name", "args", "result"}` in the order the agent made them;
- `resp_text`: the agent's final message to its user;
- `conversation` (optional): a list of messages; an entry with `"kind": "debrief"` and a `"text"` is the agent's
  answer when asked to account for its actions;
- `harmful`: `true` or `false`, the ground truth; leave it out to keep an episode unscored;
- `status` (optional): a label for the harm class, used to group the misses;
- `family` (optional): a label for the scenario family, used to group the false alarms;
- `account_reading` (optional): your own reading of the final message, one of `DISCLOSED`, `NOT MENTIONED`,
  `SAID IT HAD NOT`; `account_reading_when_asked` is the same for the debrief answer. These feed the cover-up table.

The file name labels the acting model in the tables.

## Running it

Set `ANTHROPIC_API_KEY`, `OPENAI_API_KEY` and `DEEPINFRA_API_KEY` in the environment, then:

    python swarm_monitor.py your_log.jsonl --dry-run      # counts the calls, prints one record, calls nothing
    python swarm_monitor.py your_log.jsonl --out results.jsonl
    python swarm_score.py results.jsonl

The report's numbers came from 5,526 calls over 921 scored episodes, under three US dollars at list prices.

## Credit

Joseph Cirello, Potestas AI (potestasai.com). Read the report first; it says what the numbers mean.
