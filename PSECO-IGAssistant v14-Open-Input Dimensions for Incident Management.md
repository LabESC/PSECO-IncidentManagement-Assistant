# PSECO-IGAssistant v14 — Open-Input Context Capture for Incident Management

## Overview

**PSECO-IGAssistant** is an intelligent incident management guidance system that uses open-ended questions, contextual analysis, and strategy recommendation to help organizations improve their incident response capabilities.

The v14 prototype features a streamlined 3-question interface that captures incident context through natural conversation, identifies relevant contextual characteristics (CTX), recommends an appropriate incident management strategy, and generates a personalized playbook with actionable SRE practices.

## User Journey

```
Question Input (3 questions + audio + documents)
         ↓
Context Analysis (CTX identification)
         ↓
Strategy Recommendation (with clarification if needed)
         ↓
Strategy Validation (user agreement)
         ↓
Playbook Generation (SRE practices + implementation steps)
```

## Architecture: 5 Screens

### Screen 1: Scenario Input

**Purpose:** Capture incident context through 3 open-ended questions

**Components:**
- Wordmark with version badge (v14)
- Stepper showing progress (1/5)
- 3 open-ended question textareas
- Audio recording capability for each question
- Optional document upload
- Reset and Analyze buttons

**Questions:**

#### Question 1. Technical Dimension: Incident, Service, and Operational Impact

**Prompt:**
> Describe the technical situation involved in the incident.
> 
> Please mention, if relevant, the affected service, component, software asset, environment, or dependency; what failure, degradation, or abnormal behavior was observed; whether recent changes, releases, integrations, or maintenance activities are involved; and what technical impact is most relevant, such as availability, performance, security, data integrity, reliability, scalability, metrics, or operational stability.

**Input Method:** Text, audio recording, or combination

#### Question 2. Business Dimension: Governance, Ecosystem Actors, and Responsibilities

**Prompt:**
> Describe the business and governance conditions that may affect the response.
> 
> Please mention, if relevant, which ecosystem actors need to be involved, whether the response depends on a central organization, supplier, partner, or customer, and whether there are access restrictions, approvals, contracts, licenses, compliance requirements, unclear responsibilities, ownership issues, or possible business ripple effects.

**Input Method:** Text, audio recording, or combination

#### Question 3. Social Dimension: Team, Leadership, and Response Conditions

**Prompt:**
> Describe how people, teams, and leadership are handling the response.
> 
> Please mention, if relevant, whether communication and collaboration are working well, whether people feel safe to raise concerns, escalate issues, or ask for help, whether leadership provides clear direction, support, and autonomy, and whether the team is overloaded, under pressure, or working in an unsustainable way.

**Input Method:** Text, audio recording, or combination

**Validation:** At least 1 question must be answered to proceed

**Optional Upload:** Supporting documents (incident reports, architecture diagrams, postmortems, etc.)

---

### Screen 2: Contextual Characteristics Identified

**Purpose:** Display identified contextual characteristics (CTX) based on scenario analysis

**Components:**
- Stepper showing progress (2/5)
- Title: "Contextual Characteristics Identified"
- Table with 3 columns: CTX ID | Characteristic | Evidence
- Back and Proceed buttons

**CTX Mapping Logic:**

The system analyzes the user's responses for keywords and phrases to identify relevant contextual characteristics:

| CTX ID | Characteristic | Associated Keywords | Primary Strategy |
|--------|---|---|---|
| CTX01 | Insufficient traceability of the affected software asset | unknown asset, unclear owner, version unknown | T5 |
| CTX02 | Dependency among ecosystem actors affects the incident response | external providers, partners, ecosystem | T4 |
| CTX03 | Handoffs or collaboration arrangements make the response slow, fragmented, or inconsistent | fragmented, slow, handoffs, silos | T3 |
| CTX04 | Dependence on the central organization for approval, access, or response authority | approval required, central org, access restrictions | T1 |
| CTX05 | Technological variability or compatibility restrictions increase operational risk | multiple technologies, compatibility, versions | T7 |
| CTX06 | Insufficient metrics to assess impact and response effectiveness | metrics, dashboards, monitoring | T2 |
| CTX07 | Low visibility into systemic effects before acting | visibility, ripple effects, systemic | T2 |
| CTX08 | Incident associated with maintenance, evolution, or component obsolescence | maintenance, outdated, evolution | T7 |
| CTX09 | Resolution is hindered by a shared knowledge gap | knowledge gap, unclear, documentation | T5 |
| CTX10 | New component, actor, or change must comply with entry, quality, or compliance rules | new component, compliance, quality | T7 |
| CTX11 | Feedback, perception, or visibility from affected users/stakeholders is not being captured | user feedback, stakeholder feedback | T8 |
| CTX12 | Low psychological safety to discuss causes, failures, and learning after the incident | safe, blame, reluctant | T6 |
| CTX13 | Communication and collaboration among the involved actors are not working well | communication, collaboration, unclear | T4 |
| CTX14 | Leadership does not provide sufficient direction, support, or autonomy for the response | leadership, direction, support, autonomy | T1 |
| CTX15 | Response occurs under overload, excessive pressure, or low work sustainability | pressure, overload, reactive, unsustainable | T3 |

**Default Behavior:** If no CTX are identified, system defaults to CTX02 and CTX13 (multi-team involvement and coordination challenges)

---

### Screen 3: Clarification Question (Conditional)

**Purpose:** Refine strategy recommendation when multiple strategies have equal priority

**Trigger:** Appears only if 2+ strategies tie for highest CTX frequency

**Components:**
- Stepper showing progress (3/5)
- Single open-ended question
- Textarea for response
- Back and Continue buttons

**Question:**
> What would most immediately improve the incident response in this situation?
> 
> Please explain whether the priority is to formalize responsibilities and response paths, improve visibility and monitoring, automate manual work, coordinate actors, organize knowledge, learn from the incident, manage a change-related issue, or capture feedback from affected users or stakeholders.

**Keyword Mapping:**
- "coordinate" / "collaboration" / "team" → T4
- "monitor" / "visibility" → T2
- "automate" → T3
- "formalize" / "plan" → T1
- (default) → T4

---

### Screen 4: Strategy Validation

**Purpose:** Confirm the recommended strategy with user and allow feedback

**Components:**
- Stepper showing progress (4/5)
- Recommendation box displaying strategy (T1-T8)
- Validation question with Yes/No radio buttons
- Conditional feedback textarea (appears if "No" is selected)
- Back and Proceed buttons

**Recommendation Box Content:**
```
[Strategy ID] — [Strategy Name]
This strategy was selected based on the contextual characteristics identified in your scenario.
```

**Validation Question:**
> Do you agree with this strategy?

**Options:**
- Yes — This strategy is appropriate for my scenario.
- No — I would like to provide additional information to reconsider.

**Conditional Feedback (if "No"):**
> Please provide additional context or clarification:
> 
> Explain what aspects of the recommended strategy do not align with your scenario, or provide any missing information that could help refine the recommendation.

**Button Logic:**
- "Proceed to Playbook" button is disabled until user selects Yes or provides feedback for No

---

### Screen 5: Recommendation Playbook

**Purpose:** Present personalized incident management playbook based on selected strategy

**Components:**
- Stepper showing progress (5/5)
- Title: "Incident Management Playbook"
- Recommended Strategy section
- Confirmed Contextual Characteristics table
- Your Scenario Summary (user responses)
- SRE Practice section with implementation steps
- Final disclaimer
- Start Over and Print buttons

**Content Sections:**

#### 5.1 Recommended Strategy

Displays:
- Strategy ID (T1-T8)
- Strategy name

#### 5.2 Confirmed Contextual Characteristics

Table with 2 columns: CTX ID | Characteristic

Lists all CTX identified in Screen 2

#### 5.3 Your Scenario Summary

Displays user responses in formatted boxes:
- **Incident Description and Impact:** [Q1 response]
- **Governance, Dependencies, and Software Assets:** [Q2 response]
- **Team, Leadership, and Response Conditions:** [Q3 response]

#### 5.4 SRE Practice

Single SRE practice associated with the strategy, containing:

**Practice Name:** [Descriptive title]

**Implementation Steps (max 3):**

Each step includes:
1. **Step Title:** [Concise action]
2. **Description:** [Detailed explanation of what to do]
3. **Acceptance Criterion:** [Measurable success indicator]

**Example (T4 — Cross-functional Collaboration):**

**SRE Practice:** Define cross-functional incident response teams

**Step 1:** Identify stakeholders and teams involved in incident response
- **Description:** Map all teams and stakeholders that need to be involved in incident response, including infrastructure, application, database, security, and customer support teams.
- **Acceptance Criterion:** All stakeholders and teams involved in incident response are identified and documented

**Step 2:** Establish single incident coordination channel
- **Description:** Create a dedicated communication channel (e.g., Slack channel, war room) for incident coordination where all teams can collaborate in real-time during incidents.
- **Acceptance Criterion:** Incident coordination channel is established and team members are trained on its use

**Step 3:** Define decision-making authority and escalation paths
- **Description:** Clearly define who has authority to make critical decisions during incidents and establish escalation paths when decisions require higher-level approval.
- **Acceptance Criterion:** Decision-making authority is clear and escalation paths are documented and tested

#### 5.5 Final Disclaimer

> This playbook was generated based on your scenario analysis and the identified contextual characteristics. Please adapt the recommendations to your specific organizational context and incident response procedures.

---

## 8 Incident Management Strategies (T1-T8)

### T1: Establish Incident Response Plans

**Guideline:** G1 — Formalize Incident Response Procedures

**Primary CTX:** CTX04, CTX14

**SRE Practice:** Define clear incident severity levels and response procedures

**Implementation Steps:**
1. Document current incident response process and identify gaps
2. Define roles, responsibilities, and decision authorities
3. Create incident severity classification and response procedures

---

### T2: Adopt Real-Time Incident Monitoring

**Guideline:** G2 — Implement Real-Time Monitoring and Alerting

**Primary CTX:** CTX06, CTX07

**SRE Practice:** Establish comprehensive metrics collection and dashboards

**Implementation Steps:**
1. Identify key metrics and SLIs for critical services
2. Implement monitoring infrastructure and dashboards
3. Define alert thresholds and notification rules

---

### T3: Automate Incident Management Processes

**Guideline:** G3 — Automate Incident Response Workflows

**Primary CTX:** CTX03, CTX15

**SRE Practice:** Implement automated incident detection and notification

**Implementation Steps:**
1. Identify manual incident management tasks suitable for automation
2. Develop self-healing workflows for common failure scenarios
3. Create automated status update and escalation workflows

---

### T4: Coordinate Cross-Functional Collaboration

**Guideline:** G4 — Establish Autonomous Cross-functional Teams for Incident Management

**Primary CTX:** CTX02, CTX13

**SRE Practice:** Define cross-functional incident response teams

**Implementation Steps:**
1. Identify stakeholders and teams involved in incident response
2. Establish single incident coordination channel
3. Define decision-making authority and escalation paths

---

### T5: Maintain Incident Knowledge Base

**Guideline:** G5 — Build and Maintain Incident Knowledge Repository

**Primary CTX:** CTX01, CTX09

**SRE Practice:** Establish incident documentation standards and templates

**Implementation Steps:**
1. Define incident documentation standards and templates
2. Implement searchable incident knowledge repository
3. Implement regular knowledge base maintenance and updates

---

### T6: Perform Post-Incident Reviews

**Guideline:** G6 — Conduct Blameless Post-Incident Reviews

**Primary CTX:** CTX12

**SRE Practice:** Establish blameless post-incident review culture

**Implementation Steps:**
1. Define post-incident review schedule and participants
2. Create blameless incident analysis process
3. Implement action item tracking and follow-up procedures

---

### T7: Manage Incidents Caused by Changes

**Guideline:** G7 — Integrate Change Management with Incident Response

**Primary CTX:** CTX05, CTX08, CTX10

**SRE Practice:** Establish change-to-incident correlation and tracking

**Implementation Steps:**
1. Define change impact analysis and risk assessment process
2. Implement change-to-incident correlation and tracking
3. Create automated change validation and rollback procedures

---

### T8: Collect End-User Feedback

**Guideline:** G8 — Capture and Integrate End-User Feedback

**Primary CTX:** CTX11

**SRE Practice:** Establish user feedback collection mechanisms

**Implementation Steps:**
1. Define user feedback collection channels and mechanisms
2. Create user impact assessment and communication templates
3. Implement feedback-driven incident response improvements

---

## Design System

### Colors

| Token | Value | Usage |
|-------|-------|-------|
| Primary | #2563eb | Buttons, links, active states |
| Primary Hover | #1d4ed8 | Button hover state |
| Primary BG | #eff6ff | Recommendation boxes, highlights |
| Success | #16a34a | Confirmation, checkmarks |
| Background | #f8fafc | Page background |
| Surface | #ffffff | Cards, containers |
| Surface 2 | #f1f5f9 | Secondary containers |
| Text | #0f172a | Primary text |
| Text 2 | #334155 | Secondary text |
| Text 3 | #64748b | Tertiary text |
| Border | #e2e8f0 | Dividers, borders |

### Typography

- **Font Family:** Inter (sans-serif), JetBrains Mono (monospace)
- **Headings:** 800 weight, -0.02em letter-spacing
- **Labels:** 600 weight
- **Body:** 400 weight, 1.55 line-height
- **Monospace:** Used for CTX IDs and technical references

### Components

- **Buttons:** 10px vertical padding, 20px horizontal, 9px border-radius
- **Textareas:** 100px minimum height, 95% font-size
- **Cards:** 28px padding, 13px border-radius, subtle shadow
- **Tables:** Hover effect on rows, 2px bottom border on headers

### Animations

- **Terminal Loading:** Staggered line animations (600ms each)
- **Button Interactions:** 160ms ease-out transitions
- **Audio Recording:** Color change feedback (red for recording, green for saved)

---

## Interaction Flows

### Happy Path (with agreement)

1. User fills Q1, Q2, Q3 (at least 1 required)
2. System analyzes and identifies CTX
3. System recommends strategy (no clarification needed)
4. User agrees with strategy
5. System generates playbook
6. User can print or start over

### Clarification Path (tied strategies)

1. User fills Q1, Q2, Q3
2. System identifies CTX
3. Multiple strategies tie for priority
4. System asks clarification question
5. User answers clarification
6. System selects strategy based on answer
7. User validates strategy
8. System generates playbook

### Feedback Path (user disagrees)

1. User fills Q1, Q2, Q3
2. System identifies CTX and recommends strategy
3. User disagrees with strategy
4. User provides additional feedback
5. System recalculates CTX (simulated)
6. System recommends potentially different strategy
7. User validates new strategy
8. System generates playbook

---

## Audio Input

- **Supported:** All 3 questions support audio recording
- **Mechanism:** Browser MediaRecorder API
- **Format:** WAV audio
- **Controls:** Record, Stop, Re-record, Clear buttons
- **Playback:** HTML5 audio player with controls
- **Combination:** Users can mix text + audio for single question

---

## Document Upload

- **Optional:** Not required to proceed
- **Supported Formats:** PDF, DOC, DOCX, TXT, MD, PNG, JPG, JPEG
- **Display:** File list with document names
- **Purpose:** Provide organizational context for analysis
- **Examples:** Incident reports, architecture diagrams, postmortems, escalation matrices

---

## Terminal Loading UI

- **Trigger:** When analyzing scenario or generating playbook
- **Style:** macOS-style terminal window (dark background)
- **Animation:** Staggered line animations with checkmarks
- **Duration:** ~4-5 seconds per operation
- **Messages:** Contextual progress indicators

---

## Responsive Design

- **Mobile:** Adjusted padding, smaller fonts, stacked layout
- **Tablet:** Medium padding, readable font sizes
- **Desktop:** Full layout with 880px max-width container

---

## Accessibility

- **Keyboard Navigation:** All interactive elements are keyboard accessible
- **Focus Rings:** Visible outline-ring/50 on focused elements
- **Color Contrast:** WCAG AA compliant
- **Labels:** All form inputs have associated labels
- **Semantic HTML:** Proper heading hierarchy, form structure

---

## Print Support

- **Hide Elements:** Stepper, buttons, terminal overlay hidden in print
- **Optimize:** Readable font sizes, high contrast
- **Content:** Full playbook content preserved

---

## Version History

| Version | Changes |
|---------|---------|
| v1-v8 | Initial prototypes with 4 questions, document upload, validation |
| v9 | Open-input architecture with keyword analysis |
| v10 | Audio input, improved validation, comprehensive playbook |
| v11 | Document upload after strategy selection, restructured SRE practices |
| v12 | Removed document upload screen, simplified to 5 teas |
| v13 | **Merged Q2+Q3 into single question, 3-question interface, more natural interaction** |
| v14 | 3-question interface, more natural interaction, software ecosystems dimensions |

---

## Next Steps & Enhancements

1. **Backend Integration:** Connect to real analysis engine
2. **NLP Analysis:** Implement actual natural language processing for CTX identification
3. **Document Analysis:** Parse uploaded documents for enhanced context
4. **Strategy Variants:** Support multiple strategies per scenario
5. **Feedback Loop:** Track user satisfaction with recommendations
6. **Export Options:** PDF, Word, JSON export of playbooks
7. **History:** Store and compare previous analyses
8. **Collaboration:** Share playbooks with team members
9. **Customization:** Allow organizations to customize strategies
10. **Integration:** Connect to incident management platforms (PagerDuty, Opsgenie, etc.)
