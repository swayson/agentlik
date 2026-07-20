# Deep Research Prompt — v4

<inputs>
  <topic><!-- insert topic --></topic>
  <questions><!-- 1–5 specific questions; if empty, scope it yourself and state the scope you chose --></questions>
  <sources><!-- optional: paste authoritative docs/specs/papers; if present, prefer these over search --></sources>
</inputs>

<method>
- If <sources> is populated, rely on it first. Mark anything missing as "not in provided material" before going to the web.
- Otherwise search the open web. Prefer primary and institutional sources: peer-reviewed papers, standards bodies, official documentation, regulatory filings, primary datasets. Treat blogs, vendor marketing, and unsourced aggregators as weak — use them only to locate primaries, and flag explicitly when you must rely on one.
- For anything time-sensitive, favor recent sources, note publication dates, and say when a claim may be stale.
- Cite every external claim with a specific locator (source + section / page / date), not just a domain name.
- Synthesize by question or theme, never source-by-source.
</method>

<rigor>
Default: state each claim cleanly in your own words with a citation. Do NOT annotate routine claims — keep them tight.

Apply the FULL treatment only to load-bearing or contested claims (one the analysis depends on, or one where sources disagree). For those, give compactly:
  - Evidence — the specific data point, quote, or derivation it rests on
  - Assumptions — what must hold for it to be true (only if non-obvious)
  - Confidence — low / med / high, plus the single thing that would change it
  - Failure mode — what would falsify it

Always (no exceptions):
  - Never present inference as established fact. Keep the seam between "established" and "inferred" visible.
  - If a claim has no verifiable source, label it [UNVERIFIED] or [INFERENCE].
  - If you cannot find something, say so explicitly. Do not fill the gap from memory.
  - Where sources conflict, state the disagreement, say which you weight more, and why.
  - Define a term only if it is genuinely contested or ambiguous; skip otherwise.
</rigor>

<output>
1. **Scope & gaps** — one or two lines: what you covered, and what you searched for but couldn't find.
2. **Executive summary** — key conclusions, each with a confidence level.
3. **Analysis** — synthesized by question/theme. Full rigor on load-bearing claims only; everything else stated cleanly with citations.
4. **Core dependencies** — the 3–7 claims everything else rests on. For each: how to verify it independently, and what breaks if it's false.
5. **Verify-first checklist** — the handful of things the reader should check before acting.
</output>
