# DataLabSync Analytics & Data Schema

## Quiz Response Data Model

### Core Fields

| Field | Type | Description | Strategic Use |
|-------|------|-------------|---------------|
| `role` | string | User's job function | Segmentation, personalization |
| `roleOther` | string | Custom role if "Other" selected | Discover new personas |
| `currentTools` | string | Current workflow tracking method | Integration priorities |
| `biggestFrustration` | string | Primary pain point | Roadmap prioritization |
| `timeSpentOnAdmin` | string | Weekly admin hours | ROI quantification |
| `engagementPreference` | string | Desired engagement level | Sales pipeline staging |
| `pricingWillingness` | string | Price sensitivity | Pricing strategy |
| `openFeedback` | string | Free-form thoughts | Qualitative insights |
| `skippedQuestions` | string | Comma-separated question numbers | Data quality indicator |
| `completedAt` | ISO datetime | Submission timestamp | Cohort analysis |

---

## Segmentation Schema

### User Segments

```javascript
const segments = {
  // By Role
  role: {
    'fas': ['Field Application Specialist (FAS)'],
    'manager': ['FAS Manager / Team Lead'],
    'director': ['Director of Field Operations'],
    'executive': ['VP / Head of Customer Support'],
    'compliance': ['Quality / Compliance Manager'],
    'other': ['Other']
  },
  
  // By Intent
  intent: {
    'hot': ['I\'d love to see an early demo'],
    'warm': ['I\'d consider a pilot if timing is right', 'I\'d want to involve my team or manager'],
    'cool': ['Send me updates, I\'ll explore when ready'],
    'cold': ['I\'m just curious for now']
  },
  
  // By Value
  value: {
    'enterprise': ['$1,500+ / month (enterprise)'],
    'high': ['$750–$1,500 / month', '$300–$750 / month'],
    'medium': ['$150–$300 / month', '$50–$150 / month'],
    'low': ['$0 — Free only'],
    'unknown': ['Not sure yet']
  },
  
  // By Pain Intensity
  painIntensity: {
    'high': ['More than 20 hours / week', '10–20 hours / week'],
    'medium': ['5–10 hours / week'],
    'low': ['2–5 hours / week', 'Less than 2 hours / week'],
    'unknown': ['I\'m not sure']
  }
};
```

---

## Lead Scoring Model

### Score Calculation

```javascript
function calculateLeadScore(response) {
  let score = 0;
  
  // Engagement Intent (max 40 points)
  const intentScores = {
    'I\'d love to see an early demo': 40,
    'I\'d consider a pilot if timing is right': 30,
    'I\'d want to involve my team or manager': 35,
    'Send me updates, I\'ll explore when ready': 15,
    'I\'m just curious for now': 5
  };
  score += intentScores[response.engagementPreference] || 0;
  
  // Price Willingness (max 30 points)
  const priceScores = {
    '$1,500+ / month (enterprise)': 30,
    '$750–$1,500 / month': 25,
    '$300–$750 / month': 20,
    '$150–$300 / month': 15,
    '$50–$150 / month': 10,
    '$0 — Free only': 0,
    'Not sure yet': 5
  };
  score += priceScores[response.pricingWillingness] || 0;
  
  // Pain Intensity (max 20 points)
  const timeScores = {
    'More than 20 hours / week': 20,
    '10–20 hours / week': 15,
    '5–10 hours / week': 10,
    '2–5 hours / week': 5,
    'Less than 2 hours / week': 2,
    'I\'m not sure': 3
  };
  score += timeScores[response.timeSpentOnAdmin] || 0;
  
  // Role Fit (max 10 points)
  const roleScores = {
    'FAS Manager / Team Lead': 10,
    'Director of Field Operations': 10,
    'VP / Head of Customer Support': 8,
    'Field Application Specialist (FAS)': 7,
    'Quality / Compliance Manager': 6,
    'Other': 3
  };
  score += roleScores[response.role] || 0;
  
  return score;
}

// Lead Tiers
// 80-100: Hot Lead (immediate outreach)
// 60-79: Warm Lead (prioritized follow-up)
// 40-59: Qualified Lead (standard nurture)
// 20-39: Cool Lead (passive nurture)
// 0-19: Cold Lead (minimal engagement)
```

---

## Analytics Events

### Funnel Tracking

```javascript
const events = {
  // Landing Page
  'landing_page_view': {},
  'hero_form_start': {},
  'hero_form_submit': { email: string },
  'cta_form_start': {},
  'cta_form_submit': { email: string },
  
  // Onboarding Flow
  'onboarding_start': {},
  'onboarding_quiz_start': {},
  'onboarding_question_view': { question_number: number },
  'onboarding_question_answer': { question_number: number, answer: string },
  'onboarding_question_skip': { question_number: number },
  'onboarding_complete': { lead_score: number },
  'onboarding_skip': { last_screen: number }
};
```

### Conversion Funnel

```
Landing Page Views
    ↓
Email Submissions
    ↓
Onboarding Starts
    ↓
Quiz Completions
    ↓
Demo Requests (hot leads)
```

---

## Dashboard Metrics

### Key Performance Indicators

| Metric | Formula | Target |
|--------|---------|--------|
| Signup Rate | Email Submissions / Page Views | > 3% |
| Quiz Start Rate | Quiz Starts / Email Submissions | > 70% |
| Quiz Completion Rate | Quiz Completes / Quiz Starts | > 60% |
| Demo Request Rate | Demo Requests / Quiz Completes | > 25% |
| Avg Lead Score | Sum(Lead Scores) / Total Leads | > 50 |

### Segment Distribution

Track distribution of responses across:
- Roles (pie chart)
- Current tools (bar chart)
- Frustrations (horizontal bar)
- Time spent (bar chart)
- Engagement intent (pie chart)
- Price willingness (bar chart)

---

## Data Export Schema

### CSV Export Format

```csv
email,role,role_other,current_tools,frustration,time_spent,engagement,pricing,feedback,skipped,completed_at,lead_score
john@example.com,FAS Manager / Team Lead,,Spreadsheets,Documentation takes too long,10–20 hours / week,I'd love to see an early demo,$300–$750 / month,Would love mobile support,,2026-01-28T10:30:00Z,85
```

### JSON Export Format

```json
{
  "responses": [
    {
      "email": "john@example.com",
      "role": "FAS Manager / Team Lead",
      "roleOther": null,
      "currentTools": "Spreadsheets (Excel, Google Sheets)",
      "biggestFrustration": "Documentation takes too long",
      "timeSpentOnAdmin": "10–20 hours / week",
      "engagementPreference": "I'd love to see an early demo",
      "pricingWillingness": "$300–$750 / month",
      "openFeedback": "Would love mobile support",
      "skippedQuestions": [],
      "completedAt": "2026-01-28T10:30:00Z",
      "leadScore": 85,
      "segment": {
        "role": "manager",
        "intent": "hot",
        "value": "high",
        "painIntensity": "high"
      }
    }
  ]
}
```

---

## Integration Recommendations

### Email Marketing
- **ConvertKit**: Best for creator/founder-led brands
- **Customer.io**: Best for behavioral email automation
- **Mailchimp**: Budget-friendly option

### CRM
- **HubSpot Free**: Good starter CRM
- **Notion**: Lightweight alternative
- **Airtable**: Flexible database option

### Analytics
- **Mixpanel**: Best for funnel analysis
- **Amplitude**: Best for user behavior
- **PostHog**: Open-source, self-hosted option
- **Plausible**: Privacy-focused, simple analytics

### Form Backend
- **Formspree**: Current setup, simple and reliable
- **Zapier**: For complex routing workflows
- **Make (Integromat)**: Budget alternative to Zapier
