# The pilot's two failures, rerun with traces kept

After the live pilot (`../report.md`), one more live run of
only scenarios 04 and 07 ran with `--keep-traces`, so the failures could be
diagnosed from the model's raw replies. That run's own report is
`rerun-report.md` (same commit, af4ca72). Both scenarios failed the same way
as in the pilot.

The traces were checked before commit: no configured secret's value, no
Google API key pattern and no unredacted password, token, key or secret field
appears in them.

- `04-hinglish-voice-note-run1/`: the speaker gave a day and month with no
  year, the model returned no due date, as its prompt says to, and the rule
  checks passed the entry with the required date empty and unflagged. Fixed by
  marking a missing due date for the owner.
- `07-missed-alert-causes-drift-run1/`: in job 11 the agent found the missed
  alert but its add_candidate fields used names of its own; the tool's reply
  didn't say which fields it expected, and the agent gave up. Fixed by naming the
  fields in the prompt and in every refusal.
