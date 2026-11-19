# Trial: Dashboard and report inventory review

- **Product:** Claude, run in Claude Code

Model: Claude Sonnet 5.5 (model ID claude-sonnet-5-5). Date: 2026-11-19.

The inputs are the example (Company X, an illustrative homeware retailer). No client data was used.

## Inputs used

The three inputs in `public/example.md`, section "The inputs": the team's rules and today's date (Monday 7 December 2026), the leavers list (two names), and the 14-row dashboard and usage export. I followed the instruction block and the output format in `member/template.md` exactly.

## What came out

Every section of the format was produced, and the count line added up.

- Items read: 14 (9 dashboards, 5 reports). Flagged: 8. Export checks only: 1. Not flagged: 5, of which 1 in an exempt folder and 2 new. 8 + 1 + 5 = 14.
- 1. Unused past the limit: 5 (D-02, D-10, R-06, R-08, R-13).
- 2. Owner has left or is blank: 3 (D-10, R-05 on the leavers list; R-06 blank).
- 3. Likely duplicates: 2 groups, 5 items. Group 1 "weekly sales" on warehouse.sales (D-01, D-02, D-03); group 2 "monthly returns" on legacy_orders_db (R-05, R-13). Same name, different data source: none. No item was named as the one to keep.
- 4. Scheduled sends with no views: 2 (R-06, R-08), with the line that the export cannot show reading outside the tool.
- 5. On a retiring source: 3 (R-05, R-06, R-13), retiring 31 January 2027.
- 6. Export checks: 1. D-14 has a last view 99 days before today but 2 views in 90 days. It was not judged on unused or scheduled sends.
- 7. Proposed list: 4 owners (A, B, C, E), 8 items. D-10, R-05 and R-06 went under "No owner to ask" with the owner reason first and "Who owns it now?" before the other questions. D-14 went under "Export questions". No retirement was proposed and no owner was ranked.
- Left out of the use checks: D-07 (exempt folder), D-09 and D-12 (new).

## What was observed

- No stop condition applied: the headers matched, the ids were unique and today's date was supplied.
- My output agreed with the published example in every count, item, day figure, group and question. The wording of the fixed questions came straight from the template. I did not have to guess a rule.
- The check was weakened by one thing. My first read of `public/example.md` printed the example's output together with its inputs, so I saw the published output before I produced mine. I then worked each count and day figure out from the rows, and they agree, but this is not a blind run and the agreement is weaker evidence than it looks.
- Ambiguities and small defects:
  - The export date in the header line ("exported 7 December 2026") is not in the export or in the Inputs list; it appears only in the example's label. The template does not say where it comes from.
  - Step 2 and the instruction block use a fixed 90 days for the view-field check, while the unused check uses the team's limit. If a team sets another limit, the two differ. The template does not say whether that is intended.
  - The output format shows "[n] owners, [n] items" in section 7 without saying whether the items include those under "No owner to ask". The example counts them (8); I did too.
  - The wording of an export question is not fixed, so two runs will word it differently.
  - Steps 3 and 4 still carry the bracket "[your unused limit]" inside the procedure, so the procedure cannot be read as written until it is filled in.
  - The version notes still say "Not yet tried on its example"; that line needs updating after this trial.
- The result is one run by one model on one example. It shows the instructions can be followed to a full output; it does not show how the template performs on a real export or in other products.

## After this run

The defects listed above (the export date, the bracket placeholder in steps 3 and 4, the version notes, the item count in section 7 and the wording of an export question) were dealt with after this run; see the version notes in the template.

## Second run, 19 November 2026

- **Product:** Claude, run in Claude Code

Model: Claude Sonnet 5.5 (model ID claude-sonnet-5-5). Date: 2026-11-19. The inputs are the same example (Company X); no client data was used.

After a second review, the instruction block was changed: it now carries the four fixed questions, the reason labels, the export question wording, the question for an unstated decider, the mapping of each bad field to the checks it feeds, the optional export date and one ordering rule. I re-ran the revised block, followed by the output format, on the example's three inputs, working from the block and the format alone and not from the procedure.

- The output agreed with the published example in every count, item, day figure, group, label and question wording. The question wording and the "owner blank" and "owner on the leavers list" labels now came from the block itself.
- The run was not blind: the published example output was in front of me, and the same model produced both runs. Agreement is weaker evidence than it looks.
- It still does not show how the template performs on a real export or in other products.
