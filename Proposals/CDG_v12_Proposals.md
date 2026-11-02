---
module: protocol
topic: Proposed changes for CDG v12
session: S14
tags: [added]
---

> *This is a proposal, not a rule. Nothing here changes CDG v11 until you decide. The evidence for each item comes from the friction log in your S13 handoff (the original copy, which stays where it is) and from the exam day session on 2 November 2026, which has no handoff of its own, so its entries are written out below.*

## Contents

- [[#Where this came from]] the two sources and what was left out
- [[#Proposed rules]] seven changes, each with the evidence behind it
- [[#Friction log entries from S14]] the exam day entries, in the log format
- [[#Already parked in S13]] two proposals that were already waiting

## Where this came from

The S13 handoff friction log had 18 entries and said the next session should propose folding the repeated patterns into the protocol. The repeated patterns were: an explanation repeated in the same words, unexplained names, a new style or a whole file when a snippet was wanted, and not checking the folder first. The exam day session on 2 November 2026 added more of the same, and two new ones.

## Proposed rules

1. Change the angle, never repeat the words. If the user says they do not understand, the next message uses a different route (a worked trace, a label on a box, a picture of the data) and does not reuse the earlier sentences. Evidence: S13 head, S13 flags, and on 2 November the circular list `previous` explanation.
2. Explain every name on first use. A new term, flag, function or tool is explained in plain words the first time it appears in a drill. Evidence: S13 tools and names (`iss`), S14 `static_cast` and `unsigned`.
3. Show the code, never only a fragment. When pointing at something the user wrote or was given, show it with its line and what to change, one item at a time. A bare one line excerpt is not enough. Evidence: S14 ("how the hell do you expect me to instantly know what you are talking about").
4. No new topics in the last session before an exam. That session is retest only. New material is parked, in the user's words, and not taught. Evidence: S14, where implicit linking was introduced on exam day and the user said it was adding stress.
5. Mark anything added to a drill as added. A requirement that the paper did not state (S14: one warning per tanker, with a `break`) is labelled `(added)` in the question. Evidence: S14 ("I didnt see the question saying that").
6. Look before asking. Check mounted folders and the project for a file before asking the user for it. Evidence: S13 location of the papers.
7. Compile before showing. Every code claim is compiled and run where it can be, and the file says which parts were not. Evidence: this session found no wrong snippets because each was run first, and the Windows only parts were named as not run.

## Friction log entries from S14

```
S14 | binary fields | Offered to skip the id and the stop count by reading them with the stream operator | A binary file has no spaces, so >> cannot step over fields, and the user wanted to know how to skip | Read the whole record, or read each piece with exact sizes and always read the full fixed size
S14 | seekg from the end | Used static_cast and the word unsigned | "Speak properly", "you are starting to irritate me" | The plain version: copy sizeof into a normal int, put a minus in front
S14 | list of fixes | Sent a short list of one line fixes with no code | He could not tell which line each one meant | One item at a time, his code beside the fix
S14 | implicit linking | Introduced it and the import library on exam day | "You are giving me more stress", "you have not shown me this before" | Dropped it, kept only the explicit pattern and the two batch lines; later covered it as a labelled variant when he asked
S14 | circular insert before | Started previous at the last node without saying why | "What made you deviate from the norm" | Used his previous and current norm, then his condition in the loop with no break
S14 | break in a drill | Added one warning per tanker and a break that the paper did not ask for | "I didnt see the question saying that" | Removed it and said the drill had added it
S14 | import library in the batch file | Put the import library line into a batch file for explicit linking | He thought it applied to both | Wrote the rule: only for DLLs linked implicitly, and a table of what is fixed and what comes from the question
```

## Already parked in S13

- Per session struggle logs, with the revision session as the last session.
- The rule that every drill states its time limit and carries its own struct or class when it reuses one.

---
*CDG v11 | written S14 | 2026-11-02*
