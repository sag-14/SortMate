# SortMate ♻️
### From Waste Identification to Verified Recovery

SortMate is an AI-assisted waste recovery and traceability prototype that connects **waste classification → human verification → recovery batch creation → partner matching → pickup scheduling → collection → recycler handoff → verified recovery**.

## Problem
Potentially recoverable waste is often incorrectly segregated, poorly tracked, or fails to reach the appropriate recovery partner. SortMate focuses on the missing connection between correct identification and a traceable recovery journey.

## Core Workflow
**Identify → Human Verify → Recovery Eligibility → Create Batch → AI-Assisted Partner Match → Assign Partner → Schedule Pickup → Reschedule if needed → Accept → Collect → Send to Recycler → Recover**

### 1. AI Waste Classification
- Upload/capture a waste image.
- AI-assisted category classification.
- Confidence score and explanation.
- Human confirms or corrects the result.
- Recovery eligibility is determined from the verified category.

### 2. Verification-Driven Waste Batches
A recovery batch is **not an independent data entry**. It is created from a human-verified, recovery-eligible classification.

Recovery workflow currently supports:
- Recyclable → Mixed Recyclable
- Dry → Paper/Cardboard
- E-waste → E-Waste

Wet and hazardous waste can still be classified and logged, but are not automatically routed into the current recovery-partner batch workflow.

When a batch is created, SortMate carries forward:
- Verified material
- AI confidence
- Human verification status
- Source/location
- Quantity
- Unique Batch ID

### 3. AI-Assisted Partner Matching
Each recovery-ready batch can be matched to compatible prototype partners using:
- Material compatibility
- Capacity
- Minimum quantity
- Distance/radius
- Availability
- Verification status

After assignment, the selected partner is stored against the **same waste batch**.

### 4. Pickup & Rescheduling
A matched batch automatically feeds the pickup workflow.

The pickup form inherits:
- Batch ID
- Material
- Quantity
- Source/location
- Assigned recovery partner

A pickup receives a unique **Pickup ID**.

If the schedule changes, the existing pickup can be **rescheduled without creating a new pickup record**. The same Pickup ID is retained and a reschedule event is added to the journey history.

### 5. Waste Journey
The batch follows a persistent journey:

**Created → Human Verified → Partner Matched → Pickup Scheduled → Pickup Accepted → Collected → Sent to Recycler → Recovered**

If a pickup is rescheduled, the journey records the scheduling change while retaining the underlying batch and Pickup ID.

## User Roles
### Waste Generator
Classifies waste, verifies AI results, creates recovery batches, assigns partners, schedules pickups and tracks journeys.

### Waste Picker / Collector
Can accept assigned pickups and mark collection.

### Recycler
Can receive material, send it to recycler processing and verify recovered material in the prototype workflow.

### Brand / EPR role
Can view recovery, sustainability and EPR-support reporting modules.

## Technology Stack
- HTML5
- CSS3
- JavaScript (ES6+)
- LocalStorage
- AI-assisted vision architecture
- Rule-based weighted partner matching

### AI Integration
The prototype includes an optional external vision backend hook:

`SORTMATE_AI_ENDPOINT`

When no endpoint is configured, a clearly labelled browser heuristic fallback is used for demonstration. The fallback is **not a trained computer-vision model**.

### Partner Matching
Matching is currently deterministic and explainable, using weighted rules rather than a machine-learning matching model.

## Architecture

```text
Waste Image
    ↓
AI Classification
    ↓
Human Verification
    ↓
Recovery Eligibility
    ↓
Waste Batch + Batch ID
    ↓
AI-Assisted Partner Matching
    ↓
Assigned Partner
    ↓
Pickup Scheduling
    ↓
Reschedule if needed
    ↓
Pickup Accepted
    ↓
Collected
    ↓
Sent to Recycler
    ↓
Verified Recovery
    ↓
Impact / Sustainability / EPR-support Reporting
```

## Data Flow
The current prototype is a client-side application. Workflow state is stored in browser LocalStorage.

Stored prototype state includes:
- Verification records
- Waste batches
- Partner assignments
- Pickup records
- Reschedule history
- Journey events
- Recovery information

No production backend or live logistics API is required to run the current prototype.

## Running the Project
1. Clone or download the repository.
2. Open `index.html` in a modern browser.
3. Use the interface to test the workflow.

No build step is required.

## Recommended Demo Flow
For the clearest demonstration:

1. Waste Generation
A college/office/brand facility generates recyclable waste.

2. Waste Image Upload
The waste generator uploads/captures an image of the waste.

3. AI Waste Classification
SortMate identifies the material category and provides a confidence score with an explanation.

4. Human Verification
The user confirms or corrects the AI result.

5. Recovery Eligibility
SortMate determines whether the verified material can enter the current recovery workflow.

6. Waste Batch Creation
A unique Waste Batch ID is created with:

7. AI-Assisted Partner Matching
SortMate evaluates registered recovery partners based on:

8. Partner Assignment
The suitable recovery partner is assigned to the same Waste Batch ID.

9. Pickup Scheduling
A pickup is scheduled with:

10. Pickup Acceptance & Collection
The recovery partner accepts the pickup and the batch status progresses to Collected.

11. Sent to Recycler
The collected material is transferred to the appropriate recycler, maintaining the same Batch ID and journey record.

12. Recovery Verification
The recycler confirms that the material has entered the recovery/recycling process.

13. Recovery Data Recorded

14. Brand / EPR Reporting
Aggregated verified recovery records can be used to generate sustainability and EPR-support data for brands.

## Prototype Limitations
- Frontend/client-side prototype.
- LocalStorage is used instead of a production database.
- Demo/registered prototype partners are not represented as real-world contractual partners.
- Pickup and logistics events are simulated prototype events.
- Environmental impact figures are estimates and are not independently verified recovery claims.
- EPR reporting is prototype reporting support, not a filing-ready legal compliance submission.

## Submission Context
Built for **Bit N Build '26 — UP Regionals**.

The submission package requires the project repository with README, presentation/PPT, and a demo video link.
