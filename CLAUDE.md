# Pressure Test Room — Build Instructions

## What This App Does
An AI-powered adversarial strategist that red-teams business plans 
across 4 lenses, generates a scored vulnerability report, 
then rebuilds the weakest sections.

## Framework Data
- Question bank is in /data/framework.csv
- 4 lenses: Financial Viability, Market Validity, 
  Execution Risk, Competitive Response
- Weights: Critical > High > Medium

## User Flow
1. Landing page — paste a business plan as text
2. Analysis screen — animated progress through all 4 lenses
3. Red team dashboard — 4 columns, colour-coded vulnerability cards
   Critical = red, High = amber, Medium = blue
4. Rebuild screen — AI rewrites the weakest sections
5. Before/After comparison — side by side

## Tech Stack
- NextJS 14 App Router
- Tailwind CSS  
- Anthropic SDK (model: claude-sonnet-4-20250514)
- API key from process.env.ANTHROPIC_API_KEY

## API Routes
POST /app/api/analyze/route.ts
- Input: { plan: string }
- Reads all questions from framework.csv
- Calls Anthropic API once for all 4 lenses
- Returns scored findings per lens

POST /app/api/rebuild/route.ts
- Input: { plan: string, criticalFindings: string[] }
- Returns: { improvedPlan: string, changes: string[] }

## Design
- Dark industrial theme, feels like a pressure test
- Monospace font for findings
- Severity badges: CRITICAL / HIGH / MEDIUM
- Big vulnerability score displayed prominently (0-100)
- Before/after side by side with clear diff

## Key Rule
Every finding must be specific to the submitted plan.
No generic advice. Reference actual details from the plan.
