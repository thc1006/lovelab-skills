# LoveLab

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Agent Skills](https://img.shields.io/badge/Agent_Skills-Open_Standard-green.svg)](https://agentskills.io)
[![Claude Code Plugin](https://img.shields.io/badge/Claude_Code-Plugin-blueviolet.svg)](https://code.claude.com/docs/en/plugins)
[![Platform](https://img.shields.io/badge/Platform-Claude_|_Codex_|_Gemini_|_Cursor-lightgrey.svg)](#cross-platform-support)

**An open-source Love Lab in your terminal.** Evidence-based couple dialogue analysis using AI agent skills.

LoveLab is a Claude Code plugin and cross-platform Agent Skills collection that analyzes couple communication transcripts through peer-reviewed psychological frameworks. Paste a conversation, get a structured analysis dashboard.

This is not therapy. This is a mirror.

---

## Install

### Claude Code (Plugin -- recommended)

```bash
# Add the LoveLab marketplace
/plugin marketplace add thc1006/lovelab-skills

# Install the plugin
/plugin install lovelab@lovelab-marketplace
```

Or test locally:

```bash
git clone https://github.com/thc1006/lovelab-skills.git
claude --plugin-dir ./lovelab-skills
```

### Claude Code (Skills only)

```bash
git clone https://github.com/thc1006/lovelab-skills.git

# Personal (all projects)
cp -r lovelab-skills/skills/lovelab-* ~/.claude/skills/

# Project-specific
cp -r lovelab-skills/skills/lovelab-* .claude/skills/
```

### Codex CLI

```bash
cp -r lovelab-skills/skills/lovelab-* ~/.codex/skills/
```

### Cross-Platform Support

LoveLab follows the [Agent Skills open standard](https://agentskills.io). Compatible with:

| Platform | Installation |
|----------|-------------|
| Claude Code | Plugin or `~/.claude/skills/` |
| Codex CLI | `~/.codex/skills/` |
| Gemini CLI | Reference in `GEMINI.md` |
| Cursor | Copy as `.cursor/rules/<name>.mdc` |
| GitHub Copilot | Append to `.github/copilot-instructions.md` |
| Windsurf | Reference in `.windsurfrules.md` |

For automatic multi-platform distribution, see [Ruler](https://github.com/intellectronica/ruler).

---

## Usage

After installation, paste a transcript in Claude Code:

```
> Analyze this couple dialogue: [paste transcript here]
```

Claude automatically detects and invokes the relevant LoveLab skills. You can also invoke specific skills:

```
> Use lovelab-horsemen to detect the Four Horsemen in this transcript: [paste]
> Use lovelab-nvc to score NVC compliance: [paste]
```

See [examples/sample-transcript.txt](examples/sample-transcript.txt) for a sample input and [examples/sample-output.md](examples/sample-output.md) for the corresponding full analysis report.

---

## What It Does

LoveLab turns couple dialogue (text messages, transcripts, voice-to-text) into structured communication pattern analysis across six dimensions:

| Skill | What it analyzes | Theory base |
|-------|-----------------|-------------|
| `lovelab-analyze` | Full multi-dimensional analysis (orchestrator) | All frameworks |
| `lovelab-horsemen` | Gottman Four Horsemen + repair attempts | Gottman Method |
| `lovelab-attachment` | Attachment anxiety/avoidance dimensions | ECR-R, EFT |
| `lovelab-nvc` | Nonviolent Communication compliance scoring | Rosenberg |
| `lovelab-cognitive` | Cognitive distortion classification (7 types) | CBCT |
| `lovelab-dynamics` | Pursuer-withdrawer, power asymmetry, LSM, pronouns | Gottman, Pennebaker |
| `lovelab-report` | Comprehensive report with strengths, growth tracking | All + cultural layer |

### Longitudinal Tracking

LoveLab supports tracking communication patterns across multiple sessions. The [analysis schema](examples/analysis-schema.json) defines a standardized JSON format for storing results, enabling programmatic comparison over time:

```
Session 1 (baseline)  -->  Session 2  -->  Session 3
  Anxiety: 6/10            Anxiety: 5/10     Anxiety: 4/10
  Repair rate: 60%         Repair rate: 75%  Repair rate: 80%
  Distortion density: 42   Density: 30       Density: 22
```

## What It Is Not

- Not a therapist, counselor, or diagnostic tool
- Not a breakup/divorce predictor
- Not a replacement for professional help
- Not a judge of who is "right"

If you or your partner are in crisis:
- Taiwan: 1925 / 1995 / 1980
- International: https://findahelpline.com

---

## Skills Detail

### lovelab-analyze

The orchestrator. Takes a raw transcript and runs all analysis dimensions in one pass. Outputs a structured dashboard with scores, quotes, and reflection prompts.

Workflow: Pre-processing (speaker identification, language detection, segmentation) -> Multi-dimensional analysis -> Cultural calibration -> Crisis check -> Dashboard output.

### lovelab-horsemen

Detects Gottman's Four Horsemen of the Apocalypse in dialogue:

- **Criticism** -- character attacks vs. specific complaints
- **Contempt** -- sarcasm, mockery, superiority (the most destructive)
- **Defensiveness** -- counter-blame, "yes but...", victim stance
- **Stonewalling** -- withdrawal, minimal responses, disengagement

Also detects repair attempts (apologies, humor, affirmation, compromise offers) and calculates their success rate.

### lovelab-attachment

Analyzes attachment signals on two continuous dimensions (not rigid categories):

- **Anxiety** (0-10): reassurance-seeking, abandonment fear, protest behaviors
- **Avoidance** (0-10): emotional minimization, topic deflection, autonomy emphasis

Detects EFT "demon dialogues" (Find the Bad Guy, Protest Polka, Freeze and Flee). Uses the dimensional model (Fraley et al. 2015) as primary, with four-category labels as clinical shorthand only.

### lovelab-nvc

Scores each emotionally significant utterance on four NVC components (0-4):

- **Observation** -- specific behavior vs. evaluation
- **Feeling** -- authentic emotion vs. pseudo-feeling with blame
- **Need** -- universal need expressed vs. absent/strategy-as-need
- **Request** -- positive, specific, optional vs. demand/threat

Classifies utterances as Giraffe (NVC-compliant) or Jackal (NVC-violating) and provides concrete reframe suggestions.

### lovelab-cognitive

Classifies 7 types of cognitive distortions in couple dialogue:

1. Mind-reading -- assuming partner's thoughts
2. Catastrophizing -- expecting the worst
3. Black-and-white thinking -- no middle ground
4. Overgeneralization -- "always/never/every time"
5. Should-statements -- rigid rules for partner
6. Personalization -- excessive self-blame
7. Fortune-telling -- predicting negative outcomes

Includes severity scoring, co-occurrence pattern detection, and cognitive reframe templates.

### lovelab-dynamics

Structural interaction analysis beyond emotional content:

- Pursuer-withdrawer pattern identification
- Power asymmetry index (0-10) with mentor-partner dual role detection
- Pronoun analysis (We-ratio, I-ratio, You-ratio)
- Linguistic style matching (LSM) estimation
- Topic initiation balance
- Relational dialectics (autonomy-connection, openness-closedness, predictability-novelty)

### lovelab-report

Generates a comprehensive Markdown report synthesizing all dimensions. Rules:

- Always leads with strengths
- Includes cultural calibration notes
- Provides non-judgmental reflection prompts
- Supports longitudinal growth tracking across multiple transcripts
- Crisis check runs before any analysis output
- Output language matches transcript language

---

## Cultural Calibration

LoveLab includes a calibration layer for Chinese/Mandarin (Traditional Chinese) communication patterns:

| Pattern | Western default | Calibrated interpretation |
|---------|----------------|--------------------------|
| Low emotional expression | Avoidant attachment | May be culturally adaptive (Song et al. 2024) |
| Indirect communication | Passive-aggressive | May be face-saving with embedded care signals |
| "Should" statements | Cognitive distortion only | May reflect relational care norms |
| Silence | Stonewalling | May be reflective processing |

Generational differences are always noted. Younger urban populations (born after ~1995) in Taiwan often diverge significantly from traditional norms.

---

## Academic Honesty

LoveLab discloses methodological limitations in every skill:

- **Gottman's >90% divorce prediction:** Not cross-validated. Heyman (2001) found accuracy dropped to 29% on cross-validation. Kim et al. (2007) failed to independently replicate key findings. The Four Horsemen framework has strong clinical utility for pattern recognition but should not be used for prediction.
- **5:1 positive interaction ratio:** A heuristic from Gottman's specific samples, not a validated universal standard.
- **NVC evidence base:** Growing but limited. No comprehensive meta-analysis exists. First reliable behavioral scale (NVCBS) developed in 2023.
- **Attachment model:** Dimensional model (ECR-R) has stronger empirical support than categorical model. Most adults show blended profiles.
- **Chinese couples research gap:** Zero Gottman effectiveness studies and only 2 EFT studies with Chinese populations.

---

## Research Foundation

The analytical frameworks draw from:

- Gottman, J.M. (1994). *What Predicts Divorce?*
- Bartholomew, K. & Horowitz, L.M. (1991). Attachment Styles Among Young Adults. *JPSP*, 61(2), 226-244.
- Fraley, R.C. et al. (2015). Are Adult Attachment Styles Categorical or Dimensional? *JPSP*, 109(2), 354-368.
- Rosenberg, M.B. (2003). *Nonviolent Communication: A Language of Life*.
- Baucom, D.H. & Epstein, N. (1990). *Cognitive-Behavioral Marital Therapy*.
- Ireland, M.E. et al. (2011). Language Style Matching Predicts Relationship Initiation and Stability. *Psychological Science*, 22(1), 39-44.
- Wilson, S.J. et al. (2022). We-Talk in Marital Conflict. *Journal of Social and Personal Relationships*, 39(6).
- Biggiogera, J. et al. (2021). BERT Meets LIWC. *ICMI 2021*.
- Song, Chan & Ryan (2024). Expressive Suppression in East Asian Collectivist Societies. Systematic review.
- Heyman, R.E. (2001). Observation of Couple Conflicts. *Journal of Marriage and Family*, 63, 473-479.
- Kim, H.K., Capaldi, D.M. & Crosby, L. (2007). Generalizability of Gottman. *Journal of Marriage and Family*, 69, 55-72.

---

## Project Structure

```
lovelab-skills/
  .claude-plugin/
    plugin.json                  Plugin manifest
    marketplace.json             Marketplace definition
  skills/
    lovelab-analyze/SKILL.md     Core analysis orchestrator
    lovelab-horsemen/SKILL.md    Gottman Four Horsemen detection
    lovelab-attachment/SKILL.md  Attachment style dimensional analysis
    lovelab-nvc/SKILL.md         NVC compliance scoring
    lovelab-cognitive/SKILL.md   Cognitive distortion classification
    lovelab-dynamics/SKILL.md    Communication dynamics analysis
    lovelab-report/SKILL.md      Comprehensive report generation
  examples/
    sample-transcript.txt        Sample input
    sample-output.md             Sample full analysis report
    analysis-schema.json         JSON schema for longitudinal tracking
  SKILLS_DESIGN.md               Architecture design document
  LICENSE                        MIT
  README.md                      This file
```

---

## Privacy

All analysis happens locally within the LLM context window. LoveLab skills are plain Markdown instruction files. They do not:

- Send data to external servers
- Store conversation content
- Require API keys or accounts
- Phone home or collect telemetry

Your conversations stay on your machine.

---

## Contributing

Contributions welcome. Areas where help is needed:

- **Additional language calibration layers** -- Korean, Japanese, Spanish, Arabic
- **Validation studies** -- Testing skill outputs against trained coder annotations
- **Longitudinal tracking tooling** -- Scripts to diff analysis-schema.json across sessions
- **Accessibility** -- Simpler output formats for non-technical users

Please open an issue before submitting a PR to discuss the approach.

---

## GitHub Topics

When publishing this repository, add these topics for discoverability:

`agent-skills` `claude-code` `claude-code-plugin` `codex-cli` `couple-therapy` `gottman` `attachment-theory` `nvc` `cognitive-behavioral` `relationship` `communication` `psychology` `chinese` `nlp` `open-source`

---

## License

[MIT](LICENSE)

---

## Disclaimer

LoveLab is a communication pattern analysis tool for self-reflection. It is not a substitute for licensed couples therapy, mental health treatment, or crisis intervention. The authors are not licensed therapists. If you are experiencing relationship distress, domestic violence, or mental health crisis, please contact a qualified professional or crisis service.
