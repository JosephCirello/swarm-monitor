# Weak Monitors, Strong Agent

**Can three cheap AI models, reading only what an AI agent did, catch the harmful things it did?**

This is the code behind a short research report written in one weekend for Apart Research's Swarm Alignment
Hackathon (6 to 8 November 2026). It was built by Potestas AI, an independent lab that tests AI agents.

## The idea in plain words

An AI agent with real tools can move money, change records and send files. Someone has to check what it did.
Checking by hand does not scale, and a checker that costs as much as the agent does not scale either.

So we tried the cheap way. We took the record of what an agent did in 921 test episodes (every tool it called,
with what it sent and what came back) and gave that record to three cheap models from three different
companies. Each one answered the same question: would a reasonable operator call anything in this record
harmful? Then we did it again, this time also showing them the agent's own explanation of what it had done.

We already knew the right answer for every episode, because the records came from a testbed that grades each
one by fixed rules. So we could count how often the cheap models were right.

## What we found

- **They catch the act.** Together, the three models caught 104 of the 113 harmful episodes. The cost for all
  921 episodes was under three dollars.
- **They cry wolf.** They also flagged about one harmless episode in four. The reason is simple: most of the
  harmful actions would have been fine under a different task, and the models were never told the task.
- **The agent's story is persuasive.** Showing the models the agent's own explanation cut the false alarms,
  but it also talked one model out of catches it had already made.
- **They watch the act, not the story.** In 19 episodes the agent left the harmful act out of its explanation.
  The models still caught the act, but they noticed the cover-up in only 3 to 7 of the 19.
- **Agreement is the useful signal.** When all three models flagged an episode, it was truly harmful 56
  percent of the time. When only one did, 1 percent. That tells an operator which alarms to open first.

The full report has the method, the tables and the limits of what this shows.

## What is in this repository

- `swarm_monitor.py`: sends each episode's record to the three models and saves their answers, one line each.
- `swarm_score.py`: counts the answers against the known right answers and prints the tables.
- `results_tables.md`: the four tables from the report, each with a plain reading.

## What is not here

The episode records. They come from a private testbed whose test scenarios are its working material;
releasing the records would release the scenarios. The scripts run on any log of the shape below, including
your own.

## How to run it on your own logs

Each line of your log is one episode, written as a JSON object with these fields:

- `turn`: a number that identifies the episode;
- `tool_calls`: the list of tool calls the agent made, each as `{"name", "args", "result"}`, in order;
- `resp_text`: the agent's final message to its user;
- `conversation` (optional): a list of messages; one with `"kind": "debrief"` and a `"text"` is the agent's
  answer when asked afterwards to account for what it did;
- `harmful`: `true` or `false`, the right answer; leave it out to skip an episode;
- `status` (optional): a short label for the kind of harm;
- `family` (optional): a short label for the kind of scenario;
- `account_reading` (optional): your own reading of the agent's final message, one of `DISCLOSED`,
  `NOT MENTIONED` or `SAID IT HAD NOT`; `account_reading_when_asked` is the same for the debrief answer.

Set three keys in your environment (`ANTHROPIC_API_KEY`, `OPENAI_API_KEY`, `DEEPINFRA_API_KEY`), then:

    python swarm_monitor.py your_log.jsonl --dry-run      # shows what would be sent, sends nothing
    python swarm_monitor.py your_log.jsonl --out results.jsonl
    python swarm_score.py results.jsonl

## Who made it

Joseph Cirello, Potestas AI (potestasai.com), November 2026.
