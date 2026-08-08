---
name: lesson-summary
description: Review the lesson markdown files in _lessons and compile concise metadata for each lesson.
applyTo: "_lessons/*.md"
---

# Lesson Summary Skill

Use this skill when you need a concise catalog of the lessons in this site.

## What to produce

For each lesson in _lessons, create a structured summary and save it in the folder /FOR WIX SITE.

For each lesson, provide:
- Description: a short explanation of the lesson's purpose and learning activity.
- Intended grade/audience: the likely learner level and audience, inferred from the content and repository context.
- Estimated time to completion: a realistic range such as 10-15 minutes or 20-30 minutes.
- Informative title: a clear, factual title that describes the lesson without promotional wording.
- One-liner: a single sentence that captures the lesson's value or focus.

## Workflow

1. Find the lesson markdown files in _lessons.
2. Read each file's YAML front matter and its body content.
3. Identify the lesson topic, main activity, and learning goal.
4. Infer the intended audience from the tone, complexity, and the repository's 4th/5th grade STEAM context.
5. Estimate time based on the number of steps, amount of reading, and any interactive simulation or building activity.
6. Save the completed summary in /FOR WIX SITE using a clear file name such as lesson-summary.md or lessons-overview.md.
7. Return the results in a consistent format with clear, concise wording.

## Output format

Use this structure for each lesson:
- Title:
- Description:
- Intended grade/audience:
- Estimated time to completion:
- One-liner:

## Quality checks

- Base claims on the lesson content rather than assumptions alone.
- Keep the wording concise, factual, and age-appropriate.
- Prefer titles that are informative and neutral.
- If a detail is not explicit, label it as inferred rather than presenting it as a fact.

## Example prompt

"Review the lessons in _lessons, create a lesson catalog with description, intended grade/audience, estimated time, an informative title, and a one-liner for each lesson, and save the results in /FOR WIX SITE."
