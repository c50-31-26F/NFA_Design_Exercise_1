# NFA Design Exercise 1

## Contents

- [n06/n06.jff](n06/n06.jff): JFLAP NFA for problem 6.
- [n06/n06t.txt](n06/n06t.txt): batch test strings, with accepted strings
  before rejected strings.
- [n06/n06r.md](n06/n06r.md): report, NFA diagram, and batch-run capture.

## Learning summary

The part that required the most care was identifying what the accepting
state means after the prefix `10` has been found. It is not a one-time
accepting state: its `0` and `1` self-loops preserve acceptance for every
remaining input symbol. I used AI to check the interpretation of the
automaton and to confirm how to reproduce a batch run and take a screenshot.

The most useful possible “gold-string” is `10111`. It checks that the NFA
correctly takes the path `q0 --1--> q1 --0--> q2` and then remains in `q2`
for the remaining symbols. I also included `0010` to check that a `10`
occurring later is not enough: this NFA requires the prefix to be `10`.

For future state-controller, traffic, flight, and compiler work, I will
write down every outgoing transition from each state before testing. I will
then test the boundary cases: the shortest accepted string (`10`), accepted
strings with a suffix (`101`, `100`), and strings that are close
but do not have the required prefix (`01`, `0111`, `0010`). Maintaining a
transition table and tracing the state set after every input symbol should
prevent omitted next states and mistaken early acceptance.

Additional suggested tests are:

- Accepted: `10`, `100`, `101`, `1001`, `10111`.
- Rejected: `0`, `1`, `00`, `01`, `11`, `0010`, `111010`, `0001`, `0111`.

The files use the requested zero-padded naming pattern (`n06.jff`,
`n06t.txt`, and `n06r.md`). The report’s SVG assets provide portable
pictures without depending on a particular operating system or JFLAP
installation.