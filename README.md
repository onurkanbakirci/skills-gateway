# Skill Gateway

> Intelligent skill selection system that reduces token consumption by 95%

## Quick Start

This skill helps you select the right agent skill for any task without loading all skills into context.

### Prerequisites

- None! The gateway is live at `https://openskills.space`

### Basic Usage

When you need to perform a task:

1. **Query the gateway** with your prompt
2. **Review the recommendation** - see which skill was selected
3. **Extract the content** - get the full skill documentation from response
4. **Execute your task** using the skill instructions

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

The gateway is **live and ready to use** at:
```
https://openskills.space
```

No installation or configuration needed! Just start making requests.

**Quick Start:**
```bash
# Make a POST request to the recommend-skill endpoint
curl -X POST https://openskills.space/api/recommend-skill \
  -H "Content-Type: application/json" \
  -d '{"prompt": "your task description"}'
```

For implementation details, see [IMPLEMENTATION.md](IMPLEMENTATION.md).

## Best Practices

✅ **Do:**
- Be specific in your prompts
- Check the `matchScore` to assess relevance
- Extract and use the `content` field for full skill documentation
- Trust high match scores (>80)

❌ **Don't:**
- Use vague prompts
- Ignore low match scores (<50)
- Skip the `content` field - it contains the full skill docs!
- Load all skills anyway (defeats the purpose!)

## Contributing

Contributions welcome! Ways to improve:
- Better matching algorithms
- Machine learning integration
- Performance optimizations
- Additional filter options

## License

MIT

## Links

- [Full Documentation](skill/skill.md)
- [Usage Examples](EXAMPLES.md)
- [Implementation Guide](IMPLEMENTATION.md)
- [OpenSkills Platform](https://openskills.space)
- [Reddit: Agent Skills Optimization](https://www.reddit.com/r/ClaudeCode/comments/1opxf9f/i_was_wrong_about_agent_skills_and_how_i_refactor/)

---

**Made to optimize AI agent workflows** 🚀
