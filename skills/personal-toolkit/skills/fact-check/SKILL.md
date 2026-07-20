---
name: fact-check
description: >
  Verify claims and statements from websites, papers, or text by
  cross-referencing multiple sources. Trigger when the user asks to
  fact-check, verify, or validate a claim, article, URL, or piece of text.
  Supports URL mode, inline text mode, file path mode, and interactive mode.
disable-model-invocation: true

---

# Fact Check

Verify claims and statements by cross-referencing multiple sources, assessing
confidence probabilistically, and generating a structured report.

## 1. Determine input

**URL:** `/fact-check https://example.com/article`
- Fetch content with WebFetch (or Defuddle if available)
- Extract main claims and assertions

**Text:** `/fact-check "specific claim to verify"`
- Use the provided claim directly

**File path:** `/fact-check path/to/doc.pdf`
- Read the file and extract claims

**No input / interactive:** prompt the user for content to fact-check

## 2. Extract claims

- Break content into discrete, verifiable statements
- Distinguish factual assertions from opinions
- Flag quantitative claims (numbers, dates, statistics) explicitly
- Present the list to the user and ask: verify all or specific ones?
- Ask if the user has preferred sources

## 3. Verify each claim

For each claim:

1. **Search** — use WebSearch with the claim + key terms; also search for
   contradicting evidence; target academic/authoritative sources when applicable
2. **If user specified sources** — prioritize those, but still check for contradictions
3. **Evaluate:**
   - Source credibility (primary > secondary; peer-reviewed > news > blog)
   - Publication date (prefer recent for time-sensitive claims)
   - Consensus vs outlier positions
   - Potential bias or conflicts of interest

## 4. Assess confidence (Annie Duke method)

| Range | Meaning |
|-------|---------|
| 90-100% | Multiple high-quality primary sources agree, no credible contradictions |
| 70-89% | Strong evidence, minor contradictions explained |
| 50-69% | Mixed evidence, credible sources on both sides |
| 30-49% | Weak support, significant contradictions, or low-quality sources |
| 10-29% | Strong evidence against the claim |
| 0-9% | Claim definitively false based on high-quality evidence |

Also consider: recency, expert consensus, base rates, and what is not known.

## 5. Generate report

Save to `fact-check-report-{YYYYMMDD-HHmmss}.md` in the current directory.

```markdown
# Fact Check Report
Generated: {timestamp}
Source: {URL or "User provided text"}

## Summary
- Total claims verified: X
- High confidence (70%+): X
- Medium confidence (30-69%): X
- Low confidence/False (<30%): X

## Detailed Findings

### Claim 1: "{claim text}"

**Verification Status**: Verified / Uncertain / False / Misleading

**Confidence**: X% — {one-line reason}

**Supporting Evidence**:
- [Source](URL) — {excerpt or summary}

**Contradicting Evidence**:
- [Source](URL) — {excerpt or summary}

**Analysis**:
{Nuanced explanation}

**Key Uncertainties**:
- {what is unknown or limits the evidence}

---

{Repeat for each claim}

## Overall Assessment

{Summary of document/claim credibility}

## Sources Consulted
1. [Source](URL)

## Methodology Notes
- Search terms used
- Source selection criteria
- Limitations of this fact-check
```

## 6. Present results

After saving the report:
- Show the summary counts
- Print the path to the report
- Offer to investigate specific claims further

## Rules

**Source quality:** primary > secondary; academic/peer-reviewed > news > blog;
check funding/bias; prefer recent sources for time-sensitive claims.

**Epistemic humility:** be explicit about uncertainty; do not force binary
true/false on complex claims; distinguish "no evidence found" from
"evidence of absence".

**Opinions:** mark subjective statements clearly; do not fact-check opinions as
true/false; can verify attributed quotes or whether an opinion is widely held.

**Safety:** do not fact-check personal/private information; warn when a claim
requires specialized expertise; note actively debated topics; avoid political
bias in source selection.
