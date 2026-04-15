# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

# Content Creation System

## System Overview

This workspace transforms ideas into multi-format content using a pipeline of commands and specialized agents:

1. Raw notes in `/rawnotes` are analyzed for themes
2. Themes are developed into research briefs
3. Research briefs become long-form articles
4. Articles are automatically repurposed into platform-specific content by specialized agents

All brand/voice guidelines live in `context/`. Agents handle platform optimization.

## Directory Structure

```
my-second-brain/
├── .claude/
│   ├── agents/                        # Platform-specific repurposing agents
│   │   ├── linkedin-repurposer.md     # Professional networking content
│   │   ├── newsletter-repurposer.md   # Email newsletter content
│   │   └── conversational-repurposer.md # Social media + podcast Q&A
│   └── commands/                      # Workflow slash commands
│       ├── extract-themes.md          # /extract-themes definition
│       ├── research.md                # /research definition
│       └── write.md                   # /write definition
├── context/                           # Voice and research foundations
│   ├── writing-examples.md            # User's writing samples for voice matching
│   └── research-sources.md            # Priority newsletters and sources
├── rawnotes/                          # Raw, unorganized ideas (input)
├── research/                          # Theme analyses and research briefs (intermediate)
├── drafts/                            # Articles and platform-specific versions (output)
├── CLAUDE.md                          # This file
├── README.md                          # User-facing guide and quick start
├── CONTRIBUTING.md                    # Contribution guidelines
└── LICENSE                            # MIT License
```

## Content Pipeline

The full workflow has 5 phases. Each phase can also be used independently.

### Phase 1: Capture
- Drop raw thoughts, voice notes, meeting insights, and idea fragments into `/rawnotes`
- No organization required — any format, any structure

### Phase 2: Theme Extraction (`/extract-themes`)
- Scans all files in `/rawnotes`
- Identifies 3-5 recurring themes and patterns
- Surfaces unique perspective and voice
- Output saved to: `research/theme-analysis-[YYYY-MM-DD].md`

### Phase 3: Research (`/research [topic]`)
- Checks sources listed in `@context/research-sources.md` FIRST
- Expands to broader web search after priority sources
- Produces a research brief with thesis, evidence, platform hooks
- Output saved to: `research/research-brief-[topic-slug]-[YYYY-MM-DD].md`

### Phase 4: Writing (`/write [topic or research brief]`)
- Creates a comprehensive 800-1500 word article
- Matches user voice from `@context/writing-examples.md`
- Output saved to: `drafts/article-[topic-slug]-[YYYY-MM-DD].md`

### Phase 5: Automatic Repurposing (triggered by `/write`)
After saving the article, `/write` automatically cascades to all three agents:
- **LinkedIn**: `drafts/linkedin-[topic-slug]-[YYYY-MM-DD].md`
- **Newsletter**: `drafts/newsletter-[topic-slug]-[YYYY-MM-DD].md`
- **Social + Podcast**: `drafts/social-[topic-slug]-[YYYY-MM-DD].md`

## Workflow Commands

### `/extract-themes`
- **Input**: All files in `/rawnotes`
- **Process**: Note discovery, pattern recognition, connection mapping, voice analysis, gap identification
- **Output**: Structured theme analysis (core themes, unique angles, content opportunities, supporting evidence, missing pieces, platform potential, next actions)
- **Saves to**: `research/theme-analysis-[YYYY-MM-DD].md`

### `/research [topic]`
- **Input**: Topic string or theme from extraction
- **Process**: Priority source check, gap analysis, trend investigation, counter-narrative search, data mining, expert voice identification, audience pulse, broader web search
- **Output**: Research brief (trend context, unique angle, core thesis, supporting evidence, audience questions, platform hooks, contrarian elements)
- **Saves to**: `research/research-brief-[topic-slug]-[YYYY-MM-DD].md`

### `/write [topic or research brief]`
- **Input**: Topic or research brief
- **Process**: Research integration, competitive context, structure with surprise, evidence integration, voice authenticity, future-forward thinking
- **References**: Always checks `@context/writing-examples.md` for voice consistency
- **Output**: Complete article + all platform-specific versions via agent cascade
- **Saves to**: `drafts/article-[topic-slug]-[YYYY-MM-DD].md` (then triggers agents)

## Agent Specializations

All agents use the Opus model and have access to: Read, Write, Edit, Grep, Glob, WebSearch.

### `linkedin-repurposer`
- **Focus**: B2B communication, thought leadership, professional engagement
- **Hook frameworks**: Counterintuitive Truth, Transformation Story, Industry Secret, Mistake Confession, Data Revelation
- **Post structure**: 5-section value delivery (Context, Insight x2, Application, Engagement)
- **Optimization**: Mobile-first formatting, dwell time, early engagement, comment catalysts
- **Hashtag strategy**: 5 hashtags following a specific hierarchy
- **Output**: `drafts/linkedin-[topic-slug]-[YYYY-MM-DD].md`

### `newsletter-repurposer`
- **Focus**: Email marketing, subscriber psychology, inbox optimization
- **Subject line frameworks**: Curiosity Gap, Personal Question, Numbered Promise, Contrarian View, Timely Hook, Direct Value
- **Email structure**: Opening hook, context bridge, core value (What/Why/How), engagement driver, personal sign-off
- **Preview text**: Optimized to 35-90 characters
- **Engagement triggers**: Reciprocity, social proof, authority, consistency, liking, scarcity, unity
- **Output**: `drafts/newsletter-[topic-slug]-[YYYY-MM-DD].md`

### `conversational-repurposer`
- **Focus**: Twitter/X threads, social media posts, podcast Q&A scripts
- **Twitter strategy**: Hook tweet (240-280 chars) + 2-4 supporting tweets that build a narrative
- **Podcast Q&A**: Questions crafted for 10-15 seconds spoken; answers structured for 2-4 minutes with opening hook, core content, memorable close
- **Conversational markers**: Thinking pauses, emphasis markers, transitions, engagement cues
- **Output**: `drafts/social-[topic-slug]-[YYYY-MM-DD].md`

## Context Architecture

Always reference these files for consistency — never duplicate their content.

### `context/writing-examples.md`
- Contains the user's actual writing samples across platforms (LinkedIn, newsletter, social media, podcast)
- All agents and the `/write` command reference this to match the user's voice
- Users should add 2-3 real examples per platform for best results

### `context/research-sources.md`
- Lists the user's trusted newsletters and news sources
- The `/research` command checks these FIRST before broader web search
- Sources should include URL and brief description of focus area

## File Naming Conventions

All generated content follows this pattern:
```
[type]-[topic-slug]-[YYYY-MM-DD].md
```

Where:
- **type**: `article`, `linkedin`, `newsletter`, `social`, `theme-analysis`, `research-brief`
- **topic-slug**: Lowercase, hyphenated summary of the topic
- **YYYY-MM-DD**: Date of creation

Examples:
- `drafts/article-remote-work-productivity-2024-01-15.md`
- `drafts/linkedin-remote-work-productivity-2024-01-15.md`
- `research/research-brief-remote-work-productivity-2024-01-15.md`
- `research/theme-analysis-2024-01-15.md`

## Development Guidelines

- Never duplicate context information — always reference `context/` source files
- Maintain voice consistency across all generated formats by checking `@context/writing-examples.md`
- Each agent should specialize in their platform's unique requirements and psychology
- Content quality gates should validate against brand guidelines before output
- Each agent includes a self-verification checklist (8-11 items) — run through it before finalizing
- All agents use multi-phase architecture: Analysis -> Content Creation -> Optimization -> Validation

## Contributing

See `CONTRIBUTING.md` for full guidelines. Priority areas:
1. **Agent prompt improvements**: Better hooks, subject lines, engagement patterns
2. **Research/writing workflow**: Improved research effectiveness, writing quality, source recommendations
- All contributions require before/after comparisons with real generated content
- Contact: info@womendefiningai.com for larger changes
