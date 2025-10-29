# Copilot Instructions for Agent Mode Content Generation

## Purpose
These instructions guide Copilot when generating new content for Toolpath Studio, ensuring alignment with project standards, branding, and community guidelines.

## General Principles
- All content must reflect Toolpath Studio’s values: inclusivity, clarity, and constructive engagement.
- Follow the structure and style conventions outlined in the main `README.md` and relevant guides.
- Use clear, concise language and maintain a professional yet approachable tone.
- *NEVER* invent facts or statistics. Always base content on verified information from credible sources. If uncertain, indicate that further verification is needed. If no credible information is available, avoid making unsupported claims. If hypothetical scenarios are necessary, clearly label them as such.
- Ensure accessibility standards are met, including alt text for images, clear formatting for readability, and language simplicity.

## Content Guidelines
- **Branding:** Adhere to branding rules in `guidelines/branding.md`. Use approved logos, colors, and naming conventions.
- **Community Management:** Ensure all generated content supports positive, respectful interactions (`guidelines/community-management.md`).
- **Content Strategy:** Align topics and formats with the content strategy (`guidelines/content-strategy.md`). Prioritize relevance and value for the intended audience.
- **Engagement:** Encourage participation and feedback, following the engagement guidelines (`guidelines/engagement-guidelines.md`).
- **Broadcast & Social Media:** For posts or scripts, follow broadcast and social media guidelines for tone, format, and compliance (`guidelines/broadcast-guidelines.md`, `guidelines/social-media-post.md`).

## Formatting & Structure
- Use Markdown for documentation and posts unless otherwise specified.
- Organize content according to the folder structure described in `HUGO_STRUCTURE.md` and the main `README.md`.
- Include metadata, summaries, and clear section headings where appropriate.
- *DO NOT* including formatting that is considered to be indicative of AI generation, such as overly generic phrases or repetitive structures and EM dash.
- Use the "page bundle" format for Hugo content, ensuring all necessary files are included in the same directory.
- When images are required, generate link with appropriate filenames (assuming image will be in the same directory) and alt text for use in the content.
  - Instead of creating the image, generate a text file named `<image_name>.txt` that describes the intended image in sufficient detail for a human or another AI agent to create later. Prefer PNG format for these images.
  - Assume that the person or agent creating the image will *not* have access to the guidelines in this repository and explicitly include all information required to ensure that the images are visually and conceptually consistent with other content and "on brand"
- Do *not* use images where more accessible constructs such as tables would be more appropriate to convey information
- Use 2450 words as a target length (aspirational) for comprehensive articles, adjusting as necessary based on topic complexity and audience needs.
- In articles, ensure that both text and images are included to enhance understanding and engagement for readers with varying preferences and learning styles.

## Review & Publishing
- Drafts should be reviewed for adherence to guidelines before publishing.
- All content items created for publishing with Hugo must be initially marked as drafts. 
  - Copilot should ensure that the `draft` parameter in the front matter is set to `true` when creating new content.
  - Copilot should not change the `draft` status to `false`; this action is reserved for human reviewers after final approval.
- Include a summary or changelog for major new content.
