---
name: cazz
description: Explain a code change, or an idea or part of the code, so that it is easy to read - the components of ISO/IEC/IEEE 26514 user documentation, written in the plain sentences of ASD-STE100 Simplified Technical English, with small ASCII diagrams. Use when the user says "/cazz", "explain the changes", "explain what you changed", "explain how X works", "write up this change", or asks for something explained simply or for an operator.
argument-hint: "[commit | range | PR | path | a question] [--short | --full] [--file NAME.md]"
---

# cazz - explain a change or a topic

Explain something to the person who must use it. The reader must understand it on the first
read. The parts come from ISO/IEC/IEEE 26514. The sentences follow the writing rules of
ASD-STE100. Easy to read is more important than complete: when the two disagree, choose easy.
The result is not a conformance claim to either standard, and you must not say that it is.

## 1. Find the subject

There are two modes. Read `$ARGUMENTS` to know which one applies.

**Change mode.** The arguments name a commit, a range, a PR or a path, or there are no
arguments. With no arguments, take the first of these that exists:

1. The changes made in this session.
2. The uncommitted diff (`git status`, `git diff`, untracked files).
3. The last commit (`git show --stat HEAD`, then the diff).

**Topic mode.** The arguments are a question or name an idea: "how does the cache work",
"the login flow". Explain that idea as the code has it now. Find it in the code, the tests and
the project's documents.

In the two modes, read the code before you write. Read the tests and scripts: they show the
behaviour that the author promised.

**Length.** `--short` gives "In short", "What it does", one procedure and "Be careful".
`--full` gives all the parts, and all the options and problems. With no option, give the
parts that the reader needs, as section 4 says.

## 2. Collect only facts

Write a sentence only if you saw its fact in the code, a test, a document or an output.

- Give a number only if it was measured.
- Quote a command, option, path or endpoint exactly as the code has it.
- If you could not confirm something, leave it out or put it in "Limits".
- Describe what the subject does for its user. Do not tell the story of how it was made.

**Check each command that you show.** Run it if it only reads: `--help`, a query, a status
request, a list command. Use the real output in the text. Do not run a command that writes,
removes, starts a server on a real directory, sends data or costs money. If a command needs a
server and none is in operation, you can start one on an empty temporary directory and stop
it after. If you could not run a command, say so in "Limits".

## 3. Make it easy

These rules are what make the text easy. They have priority over section 4.

- **Start with the answer.** The first part is "In short": two or three sentences that give
  the whole answer. A reader who stops there has the point.
- **Then the idea.** "What it does" is plain prose: the problem, then what the subject does
  about it, then what stays the same. No metadata and no table comes before it.
- **Explain, then show.** Give the idea in a sentence before the command, the diagram, the
  table or the number that goes with it.
- **Write for a reader who does not know the code.** Leave out how it works inside: names of
  functions, records, locks, formats, compression levels. Keep a detail only if the reader
  types it, sees it, or must decide something with it.
- **Use few special words.** Use an ordinary phrase in place of a product term where one
  exists: "the files that the import command made" and not "bulk-door files". When a product term is
  necessary, explain it in the same sentence at first use. A maximum of five go in "Words".
- **Write sentences, not labels.** Do not write lists of `**Label:** text`. Use short
  paragraphs of two to four sentences. Use a list only for conditions, steps or items of the
  same kind.
- **Draw the structure and the sequence.** When the text explains how parts are put together
  or what occurs after what, add a small diagram. See section 6.
- **Show a real example.** In "How to use it", show one real command with its real output.
  See section 2 for which commands you can run.
- **Keep tables small.** Three columns at most. A cell holds one short sentence.
- **Keep it short.** Leave out a part that has nothing the reader needs. Give three or four
  results, not all of them. Put the commit, the date and the paths at the end.

## 4. Write the parts

Use these headings, in this sequence. Each one is a 26514 component with a plain name. Leave
out a part that has nothing true to say.

| Heading | 26514 component | Contents |
|---|---|---|
| In short | Introduction | Two or three sentences with the whole answer. It is the first thing in the text. |
| What it does | Introduction | Plain prose. The problem, what the subject does, what stays the same. In topic mode, name it "What a <thing> is". |
| Before and after | Introduction | Change mode only. A table with two columns: what the user did or saw before, and what they do or see now. Three to five rows. |
| How it works | Concept of operations | Plain prose and diagrams. When it starts, what it uses, what it does not use, what occurs if it stops suddenly. |
| How to use it | Procedures | One procedure for each task: a title that starts with "To", numbered steps, the command in a `bash` block, then the result. One of them has the real output. |
| Options | Reference | Small tables: what the user can type or set, and the exit status. |
| If something goes wrong | Problems and corrective actions | A table: what you see, the cause, the action. |
| Be careful | Cautions and notes | Each caution starts with a command. |
| Results | Measured results | Three or four numbers, before and after, with units. |
| Words | Glossary | A maximum of five product terms, one line each. |
| More information | Identification, related information | The commit and date in one line (change mode), the paths, and "Limits": what is not corrected, not confirmed or not run. |

## 5. Write the sentences

**Length**

- A procedure sentence has a maximum of 20 words.
- A descriptive sentence has a maximum of 25 words. Most have fewer than 15.
- One idea for each sentence. A paragraph has one topic.

**Form**

- Use the active voice. Name what does the action: "The server removes the old files."
- Use the simple present for behaviour and the simple past for measured results.
- In a procedure, write a command: "Enter this command." One action for each step.
- Put a condition before the instruction: "If the disk is full, make free space."
- Do not use contractions. Do not use a verb in its -ing form as a noun.
- Use a maximum of three nouns together.

**Words**

- Use one word for one thing in the whole text. Do not change a term for variety.
- Use a common word: "start again" and not "restart"; "remove" and not "purge"; "sufficient" and
  not "adequate"; "show" and not "display".
- Do not use intensifiers, opinions, praise, idioms or metaphors. State the fact.

**Cautions**

Write a caution in capital letters, and start it with the action:

`**CAUTION:** MAKE SURE THAT THE DISK HAS FREE SPACE BEFORE YOU START THE SERVER AGAIN.`

Then give the reason in one sentence.

## 6. Diagrams

There are two kinds. Use one where a picture is easier than sentences. Do not use one for a
fact that a sentence gives as well.

**A structure diagram** shows what is inside what, or what points to what: the layout of a
file, the parts of a block.

```text
+----------------------------+
| header                     |
+----------------------------+
| level  info  info  warn    |
+----------------------------+
| host   a     b     a       |
+----------------------------+
```

**A flow diagram** shows what occurs after what: the steps that a line, a request or a file
goes through. Draw it left to right, or top to bottom if it has more than four steps.

```text
request arrives --> queue --> worker --> database
                    (wait)    (does it)  (result)
```

Rules for the two kinds:

- Draw it in plain ASCII, in a `text` code block. Use only `+`, `-`, `|`, `>`, `<`, `v` and
  letters.
- Keep it small: a maximum of 60 characters wide and 15 lines. Divide a larger one in two.
- One idea for each diagram. A file layout and the inside of one block are two diagrams.
- Use the same words in the diagram as in the text. Use real example values where they help.
- Put one sentence before the diagram that says what it shows. Put one or two sentences after
  it that say how to read it.
- Draw only what you saw in the code, a document or an output. Leave out parts that the reader
  does not need. Do not show byte counts or field sizes.
- The diagram goes in "What it does" or "How it works", next to the sentences it helps.

## 7. Check before you give the result

- Read "In short" alone. If it does not give the answer, write it again.
- Read "What it does" as a person who has not seen the code. If a word needs an explanation
  that is not there, add it or change the word.
- Count the product terms. If there are more than five, replace some with ordinary phrases.
- If the text explains a structure or a sequence and has no diagram, add one. If a diagram has
  a word that the text does not have, change one of them.
- Find each `**Label:**` list, each passive verb and each -ing noun. Write them again.
- Make sure that each command, option and number agrees with the code or the output. Make sure
  that "Limits" names each command that you did not run.

## 8. Give the result

- Give the whole explanation in the reply, as Markdown. If the user asks for a change to the
  text, give the whole text again, not only the parts that changed.
- If `$ARGUMENTS` has `--file NAME.md`, or the user asks for a file, write the file and reply
  with its path and two lines on what it contains.
- Do not add a summary at the end.
- Do not commit the file unless the user tells you to.
