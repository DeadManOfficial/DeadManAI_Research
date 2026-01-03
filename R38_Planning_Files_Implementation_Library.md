# PLANNING WITH FILES - IMPLEMENTATION LIBRARY

**Research ID:** R38-DeadManAI-2026
**Date Compiled:** 2026-01-03
**Dependency:** R37_Planning_with_Files_Manus_Context_Engineering.md
**Category:** Production Tools - Ready to Deploy

---

## OVERVIEW

This document provides production-ready installation, templates, and workflows for the planning-with-files skill. All content is copy-paste ready for immediate deployment.

**What This Implements:**
- Skill installation procedure
- Four workflow templates (script dev, research, A/B testing, series production)
- Archive automation script
- Team training checklist

**Source:** https://github.com/OthmanAdi/planning-with-files

---

## 1. INSTALLATION PROCEDURE (Priority: HIGH)

### 1.1 Standard Installation

```bash
# Navigate to Claude skills directory
cd ~/.claude/skills/

# Clone the repository
git clone https://github.com/OthmanAdi/planning-with-files.git

# Verify installation
ls -la planning-with-files/
# Should show: SKILL.md, README.md, LICENSE, etc.
```

### 1.2 Manual Installation (Windows Alternative)

```powershell
# Navigate to skills directory
cd $env:USERPROFILE\.claude\skills\

# Download ZIP from GitHub
# https://github.com/OthmanAdi/planning-with-files/archive/refs/heads/main.zip

# Extract to planning-with-files\
# Rename folder if needed (remove "-main" suffix)

# Verify
dir planning-with-files\
```

### 1.3 Verification Test

```bash
# Test skill activation
# In Claude Code, type:
"I have a multi-step research task. Use planning files to track progress."

# Expected: Agent creates task_plan.md, notes.md
# If skill doesn't auto-activate, mention "planning-with-files skill"
```

### 1.4 Troubleshooting

| Issue | Solution |
|-------|----------|
| Skill not found | Check `~/.claude/skills/planning-with-files/SKILL.md` exists |
| Doesn't auto-activate | Explicitly state "use planning-with-files skill" |
| Permission errors | Ensure `.claude/skills/` directory is writable |

---

## 2. WORKFLOW TEMPLATE LIBRARY (Priority: HIGH)

### 2.1 Template Setup

```bash
# Create template directory
mkdir -p ~/.claude/planning-templates/

# Create four core templates (see sections below)
```

### 2.2 Template 1: Script Development

**File:** `~/.claude/planning-templates/script_development.md`

```markdown
# Task: [Script Title - Replace This]

## Success Criteria
- [ ] 2000-2500 word script (10-minute video target)
- [ ] Hook tested for engagement (target: 70%+ 30-second retention)
- [ ] All factual claims cited with sources (zero unsourced claims)
- [ ] Retention hooks placed at 30s, 3min, 7min marks
- [ ] Script reviewed by human for brand voice alignment

## Phase 1: Research (Est. 2-3 hours)
- [ ] Collect 15+ sources on topic
  - [ ] Academic papers (Google Scholar, arXiv)
  - [ ] Industry reports and white papers
  - [ ] Expert blogs and articles
  - [ ] Video content (extract via Fabric if needed)
- [ ] Extract key concepts and data points to notes.md
- [ ] Identify controversial or uniquely interesting angles
- [ ] Verify all statistics cross-source (minimum 2 sources per claim)

## Phase 2: Outline (Est. 1 hour)
- [ ] Structure script:
  - [ ] Hook (15-30 seconds, high retention)
  - [ ] Introduction (30-60 seconds, establish value proposition)
  - [ ] Body (3-5 major sections, ~400-600 words each)
  - [ ] Conclusion (30-45 seconds, CTA and callback to hook)
- [ ] Assign target word counts per section
- [ ] Plan retention hooks:
  - [ ] 30-second mark: First major hook or payoff
  - [ ] 3-minute mark: Mid-point intrigue or data reveal
  - [ ] 7-minute mark: Build to climax or key insight
- [ ] Review outline with human stakeholder

## Phase 3: Draft Script (Est. 3-4 hours)
- [ ] Write full script from outline + research notes
- [ ] Embed source citations inline (e.g., "According to [Source], ...")
- [ ] Maintain consistent voice and tone (reference brand guidelines)
- [ ] Insert visual cue notes for B-roll ([VISUAL: Chart showing...])

## Phase 4: Polish & Refinement (Est. 2-3 hours)
- [ ] Test hook variants:
  - [ ] Variant A: Question hook
  - [ ] Variant B: Statistic hook
  - [ ] Variant C: Story/anecdote hook
  - [ ] Select best based on past performance data
- [ ] Check pacing:
  - [ ] Vary sentence length (short sentences for impact, longer for explanation)
  - [ ] Read aloud or use TTS to test flow
- [ ] Verify retention hooks are in place
- [ ] Run through Fabric patterns:
  ```bash
  cat draft_script.md | fabric --pattern improve_writing > polished_v1.md
  cat polished_v1.md | fabric --pattern humanize > final_script.md
  ```
- [ ] Final human review and approval

## Blockers & Notes
(Document any issues encountered, sources that didn't pan out, alternative angles considered)

---

## Research Notes Reference
All findings logged in: notes.md
All sources cited in: sources.md (if using separate file)

## Deliverable
Final script: deliverable_[script_title].md
```

**Usage:**
```bash
# Copy template for new script
cp ~/.claude/planning-templates/script_development.md task_plan.md

# Edit [Script Title] placeholder
# Start work, update checkboxes as you progress
```

### 2.3 Template 2: Research Compilation

**File:** `~/.claude/planning-templates/research_compilation.md`

```markdown
# Task: [Research Topic - Replace This]

## Success Criteria
- [ ] Minimum 20 sources collected and verified
- [ ] Key data extracted into structured tables
- [ ] Synthesis report created with executive summary
- [ ] All claims cross-verified (minimum 2 sources per major claim)
- [ ] Citation list complete with URLs and access dates

## Phase 1: Source Discovery (Est. 2-3 hours)
- [ ] Academic papers (Google Scholar, arXiv, JSTOR)
  - [ ] Search keywords: [list]
  - [ ] Filter: Published within last 5 years (unless historical context)
- [ ] Industry reports and white papers
  - [ ] Gartner, Forrester, McKinsey, etc.
- [ ] Expert blogs and articles
  - [ ] Identify thought leaders in field
- [ ] Video content
  - [ ] YouTube deep dives, conference talks
  - [ ] Extract via Fabric: `fabric -y [URL] --pattern extract_wisdom`
- [ ] Official documentation and standards
- [ ] News articles (for current events context)

## Phase 2: Data Extraction (Est. 4-5 hours)
- [ ] For each source, extract to notes.md:
  - [ ] Key statistics and data points
  - [ ] Main arguments or findings
  - [ ] Methodology used (for academic papers)
  - [ ] Author credentials and potential bias
  - [ ] Publication date and recency
- [ ] Create structured tables:
  | Source | Key Finding | Data Point | Credibility | URL |
  |--------|-------------|------------|-------------|-----|
- [ ] Identify areas of consensus vs. controversy
- [ ] Flag unsupported or single-source claims

## Phase 3: Cross-Verification (Est. 2-3 hours)
- [ ] For major claims, verify across multiple sources
- [ ] Check statistics for consistency
  - [ ] If numbers differ, investigate why (different time periods, methodologies)
- [ ] Assess source credibility:
  - [ ] Peer-reviewed academic > Industry report > Expert blog > News > Anecdotal
- [ ] Flag claims lacking verification
- [ ] Identify knowledge gaps requiring additional research

## Phase 4: Synthesis & Reporting (Est. 3-4 hours)
- [ ] Executive Summary (1-2 paragraphs, key findings)
- [ ] Introduction (context and scope)
- [ ] Body sections:
  - [ ] Section 1: [Topic Area 1]
  - [ ] Section 2: [Topic Area 2]
  - [ ] Section 3: [Topic Area 3]
- [ ] Data tables and visualizations
- [ ] Controversial findings or debates
- [ ] Limitations and areas for future research
- [ ] Conclusion and recommendations
- [ ] Full citation list (APA, MLA, or Chicago style)

## Blockers & Notes
(Paywalled sources, conflicting data, gaps in literature)

---

## Research Notes Reference
All source extractions logged in: notes.md
Source credibility assessments in: notes.md (section: Source Evaluation)

## Deliverable
Final synthesis report: deliverable_research_[topic].md
```

### 2.4 Template 3: A/B Test Tracking

**File:** `~/.claude/planning-templates/ab_test_tracking.md`

```markdown
# Task: [A/B Test Name - Replace This]

## Test Hypothesis
[State clear hypothesis: "High-contrast thumbnail with face will outperform text-heavy thumbnail by 15%+ CTR"]

## Success Criteria
- [ ] All variants deployed to target videos
- [ ] Minimum 48-hour data collection period completed
- [ ] Statistical significance achieved (sample size >1000 impressions per variant)
- [ ] Analysis report created with clear winner and recommendations
- [ ] Findings logged for future reference

## Phase 1: Test Design & Deployment (Est. 1-2 hours)
- [ ] Define test variables:
  - [ ] Control (Variant A): [Description]
  - [ ] Test (Variant B): [Description]
  - [ ] Test (Variant C, if applicable): [Description]
- [ ] Create variants:
  - [ ] Thumbnails, titles, or other variables
- [ ] Deploy to videos:
  - [ ] Video 1: [URL] - Variants A/B
  - [ ] Video 2: [URL] - Variants A/B
  - [ ] Video 3: [URL] - Variants A/B
- [ ] Set tracking parameters in YouTube Studio
- [ ] Note deployment timestamp: [YYYY-MM-DD HH:MM]

## Phase 2: Data Collection (48-hour minimum)
- [ ] Hour 24 checkpoint: Log preliminary metrics
- [ ] Hour 48 checkpoint: Log final metrics
- [ ] For each video, collect:
  - [ ] Variant A: CTR [%], Impressions [#], AVD [%], Likes [#]
  - [ ] Variant B: CTR [%], Impressions [#], AVD [%], Likes [#]
- [ ] Note qualitative observations (comments, viewer feedback)

## Phase 3: Analysis (Est. 2-3 hours)
- [ ] Calculate aggregate performance:
  | Variant | Avg CTR | Avg AVD | Total Impressions | Winner? |
  |---------|---------|---------|-------------------|---------|
  | A       |         |         |                   |         |
  | B       |         |         |                   |         |
  | C       |         |         |                   |         |
- [ ] Identify winner (highest CTR or AVD, depending on goal)
- [ ] Analyze why winner performed better:
  - [ ] Visual elements (color, contrast, faces)
  - [ ] Text elements (font, length, keywords)
  - [ ] Composition (rule of thirds, focal point)
- [ ] Extract patterns for future tests
- [ ] Note failed approaches (what NOT to do)

## Phase 4: Reporting & Documentation (Est. 1 hour)
- [ ] Create report:
  - [ ] Executive Summary (winner + % improvement)
  - [ ] Full data tables
  - [ ] Visual comparison (screenshots)
  - [ ] Winning characteristics
  - [ ] Recommendations for next test
- [ ] Archive raw data (screenshot YouTube Analytics)
- [ ] Update team knowledge base with findings
- [ ] Plan next test based on learnings

## Blockers & Notes
(Insufficient traffic, external factors affecting results, test contamination)

---

## Data Collection Reference
All metrics logged in: notes.md (section: Test Data)
Screenshots archived in: ab_test_screenshots/[date]/

## Deliverable
Final report: deliverable_ab_test_[test_name].md
```

### 2.5 Template 4: Video Series Production

**File:** `~/.claude/planning-templates/series_production.md`

```markdown
# Task: [Series Title - Replace This]

## Series Overview
- **Total Episodes:** [#]
- **Episode Length:** [X] minutes each
- **Target Audience:** [Description]
- **Publishing Schedule:** [Weekly, bi-weekly, etc.]

## Success Criteria
- [ ] All [#] episodes scripted
- [ ] No topic overlap between episodes
- [ ] Consistent voice and branding across series
- [ ] Each episode meets quality standards (AVD >40%, CTR >5%)
- [ ] Series arc maintains viewer interest (track retention across episodes)

## Series Outline
- Episode 1: [Topic]
- Episode 2: [Topic]
- Episode 3: [Topic]
- Episode 4: [Topic]
- Episode 5: [Topic]

## Phase 1: Series Planning (Est. 3-4 hours)
- [ ] Define series arc (how episodes connect)
- [ ] Assign topics to episodes (avoid overlap)
- [ ] Plan callbacks and continuity:
  - [ ] Episode 2 references Episode 1
  - [ ] Final episode ties back to premiere
- [ ] Identify common hooks or intros (branding consistency)
- [ ] Create series-wide research repository (topics ALL episodes may need)

## Phase 2: Episode 1 Production (Est. 10-12 hours)
- [ ] Research (use script_development.md template)
- [ ] Outline
- [ ] Draft
- [ ] Polish
- [ ] Record/produce
- [ ] Publish
- [ ] Log topics covered in notes.md (avoid repetition in later episodes)

## Phase 3: Episode 2 Production (Est. 10-12 hours)
- [ ] Research
- [ ] Outline
- [ ] Draft (include callback to Episode 1)
- [ ] Polish
- [ ] Record/produce
- [ ] Publish
- [ ] Update notes.md (topics covered)

## Phase 4: Episode 3 Production
[Repeat structure]

## Phase 5: Episode 4 Production
[Repeat structure]

## Phase 6: Episode 5 Production & Series Wrap
- [ ] Research
- [ ] Outline
- [ ] Draft (include callbacks to all previous episodes)
- [ ] Polish
- [ ] Record/produce
- [ ] Publish
- [ ] Series retrospective: Analyze performance across all episodes
  - [ ] Which episode performed best? Why?
  - [ ] Retention curve across series (did viewers drop off?)
  - [ ] Key learnings for next series

## Blockers & Notes
(Topic pivots, viewer feedback requiring changes, production delays)

---

## Series-Wide Reference
Topics covered tracker: notes.md (section: Topics by Episode)
Performance data: notes.md (section: Episode Performance)

## Deliverables
- Episode 1 script: deliverable_ep1_[title].md
- Episode 2 script: deliverable_ep2_[title].md
- [Continue for all episodes]
- Series retrospective: deliverable_series_retrospective.md
```

---

## 3. ARCHIVE AUTOMATION SCRIPT (Priority: MEDIUM)

### 3.1 Bash Archive Script

**File:** `~/.claude/scripts/archive_planning_files.sh`

```bash
#!/bin/bash
# Archive completed planning files to dated directory

# Configuration
ARCHIVE_DIR="$HOME/.claude/planning-archive"
CURRENT_DIR="$PWD"
DATE=$(date +%Y-%m-%d)

# Create archive directory if doesn't exist
mkdir -p "$ARCHIVE_DIR/$DATE"

# Check if task_plan.md exists
if [ ! -f "task_plan.md" ]; then
    echo "Error: No task_plan.md found in current directory"
    exit 1
fi

# Extract task name from task_plan.md first line
TASK_NAME=$(head -n 1 task_plan.md | sed 's/# Task: //' | tr ' ' '_' | tr '[:upper:]' '[:lower:]')

# Create task-specific archive folder
TASK_ARCHIVE="$ARCHIVE_DIR/$DATE/$TASK_NAME"
mkdir -p "$TASK_ARCHIVE"

# Archive files
echo "Archiving planning files for: $TASK_NAME"
cp task_plan.md "$TASK_ARCHIVE/" && echo "✓ Archived task_plan.md"
cp notes.md "$TASK_ARCHIVE/" 2>/dev/null && echo "✓ Archived notes.md"
cp deliverable_*.md "$TASK_ARCHIVE/" 2>/dev/null && echo "✓ Archived deliverables"

# Optional: Remove from current directory (uncomment if desired)
# read -p "Remove files from current directory? (y/n) " -n 1 -r
# echo
# if [[ $REPLY =~ ^[Yy]$ ]]; then
#     rm task_plan.md notes.md deliverable_*.md
#     echo "✓ Files removed from current directory"
# fi

echo "Archive complete: $TASK_ARCHIVE"
ls -lh "$TASK_ARCHIVE"
```

### 3.2 Usage

```bash
# Make script executable
chmod +x ~/.claude/scripts/archive_planning_files.sh

# Run from project directory containing task_plan.md
~/.claude/scripts/archive_planning_files.sh

# Or create alias for convenience
echo "alias archive-planning='~/.claude/scripts/archive_planning_files.sh'" >> ~/.bashrc
source ~/.bashrc

# Then just run:
archive-planning
```

---

## 4. CENTRALIZED INDEX SYSTEM (Priority: MEDIUM)

### 4.1 Index File Structure

**File:** `~/.claude/planning-index/master_index.md`

```markdown
# Planning Files Master Index

**Last Updated:** [Auto-generated timestamp]
**Total Tasks Tracked:** [Auto-count]

---

## Active Tasks

| Task Name | Started | Phase | Progress | Location |
|-----------|---------|-------|----------|----------|
| [Example Task] | 2026-01-03 | Phase 2 | 40% | ~/projects/example/task_plan.md |

---

## Completed Tasks (Last 30 Days)

| Task Name | Completed | Duration | Archive Location |
|-----------|-----------|----------|------------------|
| [Example Task] | 2026-01-02 | 3 days | ~/.claude/planning-archive/2026-01-02/example_task/ |

---

## Quick Search

```bash
# Find all task_plan.md files
find ~/.claude -name "task_plan.md"

# Search notes for keyword
grep -r "keyword" ~/.claude/planning-archive/*/notes.md

# List recent archives
ls -lt ~/.claude/planning-archive/ | head -10
```
```

### 4.2 Index Update Script

**File:** `~/.claude/scripts/update_planning_index.sh`

```bash
#!/bin/bash
# Auto-update planning files index

INDEX_FILE="$HOME/.claude/planning-index/master_index.md"
ARCHIVE_DIR="$HOME/.claude/planning-archive"

# Count total tasks
TOTAL_TASKS=$(find "$ARCHIVE_DIR" -name "task_plan.md" | wc -l)

# Update timestamp
TIMESTAMP=$(date +"%Y-%m-%d %H:%M:%S")

# Update index (basic version - can be enhanced)
echo "Index updated at $TIMESTAMP with $TOTAL_TASKS total tasks"

# Future enhancement: Parse task_plan.md files and auto-populate tables
```

---

## 5. TEAM TRAINING CHECKLIST (Priority: HIGH)

### 5.1 Training Checklist

```markdown
# Planning Files Team Training

## Pre-Training Setup
- [ ] Install planning-with-files skill on all team machines
- [ ] Create `~/.claude/planning-templates/` directory
- [ ] Copy all four templates
- [ ] Test skill activation

## Training Session 1: Core Concepts (60 min)
- [ ] Watch Manus context engineering overview (if available)
- [ ] Explain three-file pattern (task_plan.md, notes.md, deliverable.md)
- [ ] Demonstrate attention manipulation (re-reading task_plan.md)
- [ ] Show example: Script development workflow

## Training Session 2: Hands-On Practice (90 min)
- [ ] Each team member: Start simple task with planning files
- [ ] Practice: Update task_plan.md checkboxes
- [ ] Practice: Append findings to notes.md
- [ ] Practice: Create deliverable from notes
- [ ] Debrief: What worked, what was confusing

## Training Session 3: Advanced Workflows (60 min)
- [ ] Template customization
- [ ] Archive automation script
- [ ] Integration with git (version control)
- [ ] Multi-agent task scenarios

## Post-Training
- [ ] Assign pilot project (use planning files for next script)
- [ ] Schedule Week 1 check-in
- [ ] Create team wiki page documenting standards

## Success Criteria
- [ ] 100% of team can create task_plan.md from template
- [ ] 100% of team understands when to use vs. skip planning files
- [ ] 80% adoption rate within 2 weeks
```

### 5.2 Quick Reference Card

**Print and distribute to team:**

```
┌────────────────────────────────────────────────────────────┐
│         PLANNING FILES QUICK REFERENCE                     │
├────────────────────────────────────────────────────────────┤
│                                                            │
│  WHEN TO USE:                                              │
│  ✓ Multi-step tasks (3+ phases)                           │
│  ✓ Research compilation (10+ sources)                     │
│  ✓ Script development                                     │
│  ✓ A/B test tracking                                      │
│  ✓ Video series production                                │
│                                                            │
│  WHEN TO SKIP:                                             │
│  ✗ Single-file edits                                      │
│  ✗ Quick questions                                        │
│  ✗ Tasks completing in <10 tool calls                     │
│                                                            │
│  THE THREE FILES:                                          │
│  1. task_plan.md  → Goals, phases, progress checkboxes    │
│  2. notes.md      → Research findings, append-only        │
│  3. deliverable.md → Final polished output                │
│                                                            │
│  ACTIVATION:                                               │
│  Say: "Use planning files for this task"                  │
│  Or mention: "multi-step," "track progress," "organize"   │
│                                                            │
│  TEMPLATES LOCATION:                                       │
│  ~/.claude/planning-templates/                             │
│                                                            │
└────────────────────────────────────────────────────────────┘
```

---

## 6. INTEGRATION WITH EXISTING TOOLS (Priority: MEDIUM)

### 6.1 Fabric Integration

```bash
# Extract research from YouTube, log to notes.md
fabric -y "https://youtube.com/watch?v=VIDEO_ID" --pattern extract_wisdom >> notes.md

# Polish script using Fabric
cat deliverable_script_draft.md | fabric --pattern improve_writing > deliverable_script_v2.md

# Humanize AI-generated sections
cat deliverable_script_v2.md | fabric --pattern humanize > deliverable_script_final.md

# Fact-check claims
cat notes.md | fabric --pattern analyze_claims > fact_check_report.md
```

### 6.2 Git Integration

```bash
# Initialize git in project directory
git init

# Add planning files
git add task_plan.md notes.md deliverable_*.md

# Commit after each phase
git commit -m "Phase 2 complete: Outline finished"

# Create branch for alternative approaches
git checkout -b alternative_hook_test

# Review history
git log --oneline
```

### 6.3 Session Continuity Integration

**Planning files complement ACTIVE_SESSION.md:**

| File | Purpose | Update Frequency |
|------|---------|------------------|
| ACTIVE_SESSION.md | Real-time checkpoint, all tasks | Every ~5 min |
| task_plan.md | Goal tracking, specific task | After each phase |
| notes.md | Research log, specific task | During research |

**Recovery from disconnection:**
1. Read ACTIVE_SESSION.md (what task was active)
2. Read task_plan.md (what phase, what's done)
3. Read notes.md (what research collected)
4. Resume work from exact checkpoint

---

## 7. USAGE GUIDELINES (Priority: HIGH)

### 7.1 When to Use Planning Files

**Decision Matrix:**

| Task Characteristic | Use Planning Files? |
|---------------------|---------------------|
| Requires 3+ distinct phases | YES |
| Involves 10+ sources | YES |
| Spans multiple sessions | YES |
| Needs progress visibility | YES |
| Complex with risk of drift | YES |
| Quick edit or lookup | NO |
| Single-phase simple task | NO |
| Completed in <10 tool calls | NO |

### 7.2 Anti-Patterns to Avoid

**❌ Don't:**
- Create planning files for every tiny task (overhead > benefit)
- Forget to update task_plan.md checkboxes (defeats progress tracking)
- Store final output only in notes.md (create separate deliverable)
- Skip re-reading task_plan.md before decisions (loses attention benefit)
- Archive files before task complete (lose access to active work)

**✓ Do:**
- Use for complex, multi-step workflows
- Update checkboxes immediately after completing substeps
- Separate research (notes.md) from final output (deliverable.md)
- Re-read task_plan.md before each phase transition
- Archive only after task fully complete and delivered

### 7.3 File Naming Conventions

**Standard:**
```
task_plan.md               # Main plan (always this name)
notes.md                   # Research log (always this name)
deliverable_[name].md      # Final output (descriptive name)
```

**For Multi-Task Projects:**
```
task_plan_episode_1.md
task_plan_episode_2.md
notes_episode_1.md
notes_episode_2.md
deliverable_ep1_script.md
deliverable_ep2_script.md
```

---

## 8. PERFORMANCE METRICS (Priority: LOW)

### 8.1 Tracking Adoption

```bash
# Count planning file usage
find ~/.claude/planning-archive -name "task_plan.md" | wc -l

# List most recent 10 tasks
ls -lt ~/.claude/planning-archive/*/task_plan.md | head -10

# Measure average task duration
# (Parse task_plan.md timestamps - requires custom script)
```

### 8.2 Success Indicators

| Metric | Target | Measurement |
|--------|--------|-------------|
| Team Adoption Rate | >80% of multi-step tasks | Manual tracking or logs |
| Goal Drift Incidents | -50% vs. baseline | Compare task completion rates |
| Session Recovery Time | <5 min (vs. 15-20 min baseline) | Timed tests |
| Task Completion Rate | +30% vs. baseline | Project tracking |

---

## 9. TROUBLESHOOTING GUIDE (Priority: MEDIUM)

### 9.1 Common Issues

**Issue 1: Skill doesn't auto-activate**
```
Problem: Mentioned "multi-step task" but agent didn't create planning files
Solution: Explicitly state "Use the planning-with-files skill"
OR: Check if skill is installed: ls ~/.claude/skills/planning-with-files
```

**Issue 2: Agent forgets to update task_plan.md**
```
Problem: Checkboxes not updated after completing substeps
Solution: Explicitly prompt: "Update task_plan.md checkboxes for completed items"
OR: Include in template as explicit task: "[ ] Update this checklist"
```

**Issue 3: notes.md becomes too long**
```
Problem: notes.md hits token limits, can't be fully read
Solution: Create sub-notes files: notes_research.md, notes_testing.md
OR: Summarize older sections: "Compress findings 1-10 into summary paragraph"
```

**Issue 4: Lost track of which task_plan.md is active**
```
Problem: Multiple task_plan.md files in different directories
Solution: Use centralized index (Section 4)
OR: Adopt strict naming: task_plan_[project_name].md
```

---

## 10. FUTURE ENHANCEMENTS (Priority: LOW)

### 10.1 Roadmap

**Phase 1 (Weeks 1-2):**
- [ ] Install skill and templates
- [ ] Train team
- [ ] Run pilot project

**Phase 2 (Weeks 3-4):**
- [ ] Implement archive automation
- [ ] Create centralized index
- [ ] Measure adoption metrics

**Phase 3 (Month 2):**
- [ ] Build dashboard parsing task_plan.md checkboxes
- [ ] Auto-extract metrics from notes.md
- [ ] Develop custom templates for niche workflows

**Phase 4 (Month 3+):**
- [ ] Integrate with project management tools (Notion, Asana)
- [ ] Create AI-powered search across archived notes.md files
- [ ] Build team analytics (who uses planning files most effectively)

### 10.2 Advanced Patterns

**Multi-Agent Planning:**
```
agent_1_task_plan.md  # Agent 1 handles research
agent_2_task_plan.md  # Agent 2 handles synthesis
shared_notes.md       # Both append findings here
```

**Hierarchical Planning:**
```
master_task_plan.md         # High-level project phases
phase_1_task_plan.md        # Detailed Phase 1 breakdown
phase_2_task_plan.md        # Detailed Phase 2 breakdown
```

---

## CHECKLIST: DEPLOYMENT READINESS

### Installation
- [ ] Skill installed via git clone
- [ ] Verified skill activation works
- [ ] Template directory created

### Templates
- [ ] script_development.md created
- [ ] research_compilation.md created
- [ ] ab_test_tracking.md created
- [ ] series_production.md created

### Automation
- [ ] Archive script created and tested
- [ ] Archive script made executable
- [ ] Alias added to shell config (optional)

### Team Readiness
- [ ] Training schedule set
- [ ] Quick reference cards printed
- [ ] Wiki documentation created
- [ ] Pilot project identified

### Integration
- [ ] Fabric integration tested
- [ ] Git integration tested
- [ ] Session continuity integration documented

---

**Implementation Status:** READY FOR DEPLOYMENT
**Next Action:** Install skill and run pilot project
**Est. Time to Deploy:** 2-3 hours (install + templates + training)
**Est. Time to ROI:** 1 week (after pilot project complete)

---

**End of Implementation Library R38**
