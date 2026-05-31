# PSECO-IGAssistant

Analyze an incident scenario and receive governance-oriented recommendations for proprietary software ecosystems.

---

## SCREEN 1: ENTRY / FRAMING

### What do you need help with?

Select the primary focus for your incident analysis.

**Available Options:**
- Prioritize an incident
- Coordinate incident response
- Decide under delivery pressure
- Review governance constraints
- Reduce dependency on specialists
- Other (please describe what you need help with)

**Action:** Start scenario analysis

---

## SCREEN 2: SCENARIO INTAKE

### Scenario Description

#### Scenario title
*Text input*
Example: Payment Gateway Timeout

#### Describe the incident or situation
*Large textarea*

Helper text: Describe what happened, what is affected, and what is making the situation difficult.

#### What is your main concern right now?
*Dropdown selection*
- Reliability
- Delivery deadline
- Security
- Coordination
- Compliance
- Knowledge dependency
- Other (please describe your main concern)

---

### Incident Framing

#### Incident type
*Dropdown selection*
- Service outage
- Performance degradation
- Security vulnerability
- Failed change or release
- Third-party dependency issue

#### Perceived severity
*Dropdown selection*
- Low
- Medium
- High
- Critical

#### Business impact
*Dropdown selection*
- Low
- Medium
- High

#### Affected component
*Dropdown selection*
- Internal component
- Organization-controlled component
- Third-party-controlled component
- Multiple component groups

---

### Organization context and characteristics

Answer the following questions to help the assistant identify whether the case exhibits organization-level constraints and characteristics relevant to the scenario.

**Response format:** Yes / No

1. Are only specific internal teams or approved external parties allowed to inspect, change, or deploy the affected component?
2. Would sharing code, logs, architecture details, or incident evidence be restricted for confidentiality, IP, or trade-secret reasons?
3. Are access, responsibilities, approvals, or handoffs in this case governed by contracts, licenses, NDAs, or service agreements?
4. Is the main concern in this case to protect platform availability, security, scalability, or operational reliability?
5. Does this case involve paid external parties or commercial incentives that may affect responsibilities or response priorities?

---

### Governance conditioning factors

Answer the following questions to help the assistant identify governance-related conditions that may affect prioritization, coordination, and execution.

**Response format:** Yes / No

1. Do you have a standardized way to identify the affected software asset, its owner, version, dependencies, and usage conditions?
2. Could this incident affect, or be affected by, dependencies between internal teams, external parties, or other actors?
3. Are current collaboration arrangements helping or slowing down the response?
4. Do you need the central organization for approval, access, coordination, or technical support?
5. Does this case involve multiple technologies, versions, environments, or compatibility constraints that make coordination harder?
6. Do you have service, quality, or ecosystem health metrics to assess the impact of this incident and the effectiveness of the response?
7. Before acting, do you need to consider broader ripple effects of this decision on releases, backlog, external parties, or platform stability?
8. Is the incident related to outdated components, pending maintenance, or lack of support for system evolution?
9. Is resolution being hindered by lack of shared knowledge, training, onboarding material, or clear operational guidance?
10. Does this case involve a new component, actor, or change that still needs to meet entry rules, compliance checks, or quality standards?
11. Are communication channels, status updates, and decision visibility clear across the actors involved?

---

### Operational challenges

Rate how strongly each of the following statements applies to the current case.

**Response scale:**
- Not at all
- Moderately
- Critically

1. Release dates, delivery cadence, or business deadlines are under pressure in this case.
2. The incident has disrupted planned work or forced teams to reallocate effort.
3. It is difficult to balance immediate business demands with platform stability, security, scalability, or service reliability.
4. Coordination or decision-making is difficult because multiple teams, external parties, or stakeholders are involved.
5. There is not enough visibility into dependencies, architecture, ownership, or ripple effects to act safely.
6. The response is being affected by unclear prioritization, rework, or recurring changes in direction.
7. Communication breakdowns or misalignment between actors are making the incident harder to contain or resolve.
8. The team is overloaded or operating in a reactive mode, which makes the response less consistent.

---

### Team and leadership considerations

Rate the following team- and leadership-related conditions.

**Response scale:**
- Not at all
- Moderately
- Critically

1. Team members feel safe to raise concerns, escalate issues, or ask for help during the incident response.
2. Communication and collaboration across the people involved in the response are working well.
3. Leadership is providing clear direction, support, and enough autonomy for the team to respond effectively.
4. The team has a healthy and sustainable working environment to respond without excessive pressure, overload, or burnout.

---

**Bottom Action:** Analyze scenario

Helper text: The assistant will process your scenario, retrieve the most relevant incident management strategy and guideline, and generate an explainable recommendation package.

---

## SCREEN 3: ORGANIZATIONAL CLARIFICATION STEP

### Tailor the recommendation to your organization

**Status:**
- ✓ Strategy identified: Cross-functional incident coordination
- ✓ Guideline: G4 — Establish Autonomous Cross-functional Teams for Incident Management

The assistant identified a suitable strategy and guideline for your scenario. To adapt the implementation steps to your organization, please answer up to 3 quick questions.

---

### Question 1

**Who usually coordinates high-priority incidents in your organization, and which teams or external parties normally need to be involved?**

*Free-text response (textarea)*

**Default answer:**
In high-priority incidents, the coordination is usually led by the IT Operations Manager. The core teams typically involved are Application Support, Infrastructure/Cloud, Information Security, and the business-facing Product Manager. When the affected component is externally controlled, the third-party provider's support team must also be involved.

---

### Question 2

**How are approvals or escalations normally handled when the response depends on another team, an external provider, or restricted access?**

*Free-text response (textarea)*

**Default answer:**
Escalations are first routed to the Application Support Lead. If restricted access or production changes are required, approval must be obtained from the IT Operations Manager. When the issue depends on a third-party-controlled component, the provider must be engaged through the official service desk channel, and any critical escalation must also be communicated to the vendor manager internally.

---

### Question 3

**Which channel, document, or routine does your organization already use to coordinate incidents and communicate status updates?**

*Free-text response (textarea)*

**Default answer:**
The organization uses a dedicated Microsoft Teams bridge for critical incidents, and all official updates are registered in the Jira incident ticket. For major incidents, the status owner posts updates every 30 minutes in the Teams channel and summarizes key decisions in the Jira record.

---

**Bottom Action:** Generate tailored recommendation

---

## SCREEN 4: RECOMMENDATION WORKSPACE

### Executive Diagnosis
*(Expanded by default)*

#### Recommended Incident Management Strategy
Cross-functional incident coordination

#### Recommended Guideline
G4 — Establish Autonomous Cross-functional Teams for Incident Management

#### Fit level / confidence
High

#### Executive Summary

This scenario indicates a strong need for structured cross-functional coordination under organization-level constraints. The incident involves restricted access, third-party dependency, contractual boundaries, and delivery pressure, making ad hoc coordination risky. The recommendation focuses on bounded team autonomy, clear decision roles, and controlled escalation.

---

### Recommended Actions
*(Expanded by default)*

#### Now

1. Define a temporary incident-response structure with named coordination roles.
2. Confirm approval and escalation boundaries for the affected component.
3. Centralize communication and incident updates in a single response flow.

---

### Success Criteria and Implementation Steps
*(Expanded by default)*

#### SC1. A formal cross-functional incident-response structure exists with clear roles and decision boundaries.

**Implementation Step 1**

Define and publish a lightweight incident-response operating agreement based on the current major-incident routine of the organization. The agreement should name the incident coordinator and core response roles as described in your organization, and explicitly include external parties when the affected component is externally controlled. It should also define your organization's coordination bridge and incident record system, and establish that production changes requiring restricted access must be approved according to your escalation process, while vendor-dependent escalations must go through your official channels.

**SRE Practice:** Manage incident resolution

Use this practice to formalize the incident command structure around your organization's existing operating model. In this case, the practice is applied by turning your current major-incident routine into an explicit response agreement with named coordination roles, defined communication ownership, documented escalation boundaries, and clear organization/third-party interfaces. This reduces improvisation and ensures that incident coordination follows a repeatable structure already compatible with your organization's reality.

---

**Implementation Step 2**

Assign named owners for incident coordination, technical response, stakeholder communication, and external dependency management. Based on your organization, the coordinator should be identified, with clear escalation to the appropriate approval authority as described in your escalation process.

**SRE Practice:** Define on-call escalating

Use this practice to clarify who must be engaged, when escalation is required, and how accountability is distributed during the response. In this case, the escalation logic should reflect your organization's actual approval flow. This ensures that escalations follow your real organizational structure and approval authorities.

---

#### SC2. A documented escalation and authorization path exists for restricted or third-party-controlled assets.

**Implementation Step 1**

Create an escalation matrix with authorized internal and external actors, approval points, and response windows. Based on your organization's process, the matrix should include the escalation points and approval authorities.

**SRE Practice:** Define on-call escalating

Use this practice to operationalize your organization's real escalation path rather than an abstract one. In this case, the matrix should include the escalation points and approval authorities as described in your organization's process, ensuring that escalations are time-sensitive and aligned with your actual governance structure.

---

**Implementation Step 2**

Document who can access evidence, approve mitigation actions, and communicate status updates in restricted scenarios. Use your organization's coordination approach as the live coordination bridge and your incident tracking system as the official decision record.

**SRE Practice:** Manage incident resolution

Use this practice to ensure that response remains coordinated even when only specific actors are authorized to inspect, approve, or act. In your organization, the coordination mechanism should be used with communication ownership explicitly assigned so that status updates remain consistent.

---

#### SC3. The team learns from the incident and reduces future dependence on ad hoc coordination.

**Implementation Step 1**

Conduct a blameless post-incident review focused on coordination issues, role ambiguity, knowledge gaps, and follow-up actions. Include the teams that were part of your organization's real escalation path, including internal support teams and external parties when applicable.

**SRE Practice:** Learn with postmortem reports and Develop the blamelessness philosophy

Use these practices to turn the incident into structured learning without reinforcing fear or blame. In your organization, the post-incident review should include the teams and roles that were part of the real escalation process, ensuring that lessons are grounded in your actual incident response structure.

---

**Implementation Step 2**

Update coordination templates, escalation paths, and restricted/shared knowledge records based on the lessons learned. Ensure that your organization's coordination approach, incident tracking system, and escalation/approval flow are reflected in the updated templates.

**SRE Practice:** Learn with postmortem reports

Use this practice to convert lessons learned into reusable organizational assets. In this case, the updates should reflect your organization's real coordination bridge, incident decision trail, and actual escalation/approval flow used during the incident.

---

### Why this applies
*(Collapsed by default)*

**Key PSECO signals detected:**
- Restricted access to affected component
- Contractual constraints affecting approvals
- Third-party dependency in the response
- Reliability concern affecting platform stability
- Strong actor dependency
- Need for organization/external coordination
- Communication and transparency gaps
- Knowledge-sharing limitations
- Delivery pressure is high
- Planned work was interrupted
- Coordination difficulty across actors
- Limited visibility into ripple effects
- Collaboration is strained
- Leadership support exists, but autonomy boundaries are unclear
- Team sustainability is at risk due to reactive overload

---

### SRE Practices Involved
*(Collapsed by default)*

#### Primary SRE practices
- Manage incident resolution
- Define on-call escalating

#### Supporting SRE practices
- Learn with postmortem reports
- Develop the blamelessness philosophy

#### Why they matter in this case

These practices support clear coordination, escalation discipline, and learning after stabilization, which are essential in a PSECO scenario with multiple actors and restricted action boundaries.

---

### Anti-patterns to Avoid
*(Collapsed by default)*

- Autonomy without guardrails
- Hero culture
- Fragmented communication
- Learning without follow-through

---

### Notes and Constraints
*(Collapsed by default)*

- Access to logs is partially restricted.
- The affected component is partly controlled by an external actor.
- Local action is possible, but external approval is required for some changes.
- Coordination records should preserve traceability without exposing restricted information.

---

### Traceability and Evidence
*(Collapsed by default)*

#### Guideline ID
G4

#### Strategy ID
Cross-functional incident coordination

#### Framework elements used
- Organization characteristics
- Governance conditioning factors
- Operational challenges
- Team and leadership considerations
- SRE practices
- Success criteria and implementation steps

#### Evidence sources used
- PSECO SMS
- Incident management taxonomy
- SRE multivocal literature review
- TR4SEM framework

---

**Bottom Action:** Start new analysis

---

## NOTES ON DYNAMIC ADAPTATION

The content displayed in Screen 4 (Recommendation Workspace) is dynamically adapted based on the answers provided in Screen 3 (Organizational Clarification Step). Specifically:

- **Implementation steps** incorporate details about the organization's incident coordination structure, approval authorities, and communication channels extracted from the clarification questions.
- **SRE Practice explanations** reference the organization's specific escalation process, coordination mechanisms, and approval flow.
- **All recommendations** are contextualized to reflect the organization's actual incident management practices rather than generic guidance.

This ensures that the final recommendation is tailored to the organization's specific context and operational reality.
