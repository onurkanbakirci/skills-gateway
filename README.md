# Skill Gateway

> Intelligent skill selection system that reduces token consumption by 95%

## Quick Start

### Installation

1. Download the `skill.md` file from this repository
2. Place it in your project's skills directory
3. Start using it immediately!

### Usage

Once the skill is in your project, your AI agent can:

1. **Query the gateway** with a task prompt
2. **Receive full skill documentation** in the response
3. **Execute the task** using the returned skill instructions

## Why Use This?

**Without Gateway:**
- Load 100+ skill definitions
- Consume 500KB+ of context
- ~125,000 tokens used
- Slow, expensive, cluttered 😞

**With Gateway:**
- Query gateway: 200 tokens
- Load 1 skill: 1,250 tokens
- Total: ~1,450 tokens
- Fast, cheap, focused 🎉

**Result: 99% token savings!**

## How It Works

```
┌─────────────────┐
│  Your Task      │
└────────┬────────┘
         │
         ▼
┌─────────────────────────────┐
│   Skill Gateway API         │
│   ┌─────────────────────┐   │
│   │ 1. Fetch Skills     │   │
│   │ 2. Match Keywords   │   │
│   │ 3. Score & Rank     │   │
│   │ 4. Return Best      │   │
│   └─────────────────────┘   │
└────────┬────────────────────┘
         │
         ▼
┌─────────────────┐
│ Selected Skill  │
│ (Only load this)│
└─────────────────┘
```

## API Reference

### POST /api/recommend-skill

Find the best skill for a task and get its full documentation.

**Request:**
```json
{
  "prompt": "create a PowerPoint presentation"
}
```

**Response:**
```json
{
  "message": "Skill recommendation found",
  "recommendedSkill": {
    "id": "abc-123",
    "name": "pptx",
    "description": "Create PowerPoint presentations",
    "category": "Productivity",
    "tags": ["powerpoint", "presentation"],
    "sourceUrl": "https://github.com/...",
    "owner": "anthropic",
    "matchScore": 95,
    "content": "---\nname: pptx\n... (full skill documentation)"
  }
}
```

**Key**: Extract the `content` field to get the complete skill documentation.

See [skill/skill.md](skill/skill.md) for complete documentation.

## Live Example

```bash
curl -X POST https://openskills.space/api/recommend-skill \
  -H "Content-Type: application/json" \
  -d '{
    "prompt": "Create a PDF report with charts"
  }'
```

Response:
```json
{
  "message": "Skill recommendation found",
  "recommendedSkill": {
    "id": "d54585ee-5994-456e-bdf3-d37117eeaa1d",
    "name": "pdf",
    "description": "Generate, process, and manipulate PDF documents",
    "category": "Productivity",
    "tags": ["pdf", "documents", "processing"],
    "sourceUrl": "https://github.com/anthropics/skills/tree/main/skills/pdf",
    "owner": "anthropic",
    "matchScore": 95.5,
    "content": "---\nname: pdf\ndescription: Generate...\n(full SKILL.md content)"
  }
}
```

**Important**: Use the `content` field to access the complete skill documentation.

See [EXAMPLES.md](EXAMPLES.md) for more detailed examples.

## Service Information

The gateway API is **live and ready to use** at:
```
https://openskills.space/api/recommend-skill
```

**No server setup required!** Just download the skill file, place it in your project directory, and your AI agent will automatically use the live API to get skill recommendations.

**Quick Test:**
```bash
curl -X POST https://openskills.space/api/recommend-skill \
  -H "Content-Type: application/json" \
  -d '{"prompt": "your task description"}'
```

## Browse Available Skills

Want to explore all available AI agent skills? Check out the **[Awesome Skills](https://github.com/onurkanbakirci/awesome-skills)** repository - a curated collection you can browse, search, and download at [openskills.space](https://openskills.space).

---

**Made to optimize AI agent workflows** 🚀