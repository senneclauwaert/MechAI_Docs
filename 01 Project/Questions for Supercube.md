---
tags: [project, open, supercube]
updated: 2026-11-17
---
# Questions for Supercube

Back to [Final Work Hub](../Final%20Work%20Hub.md) · Related: [Open questions](Open%20questions.md)

This note collects everything the MechAi team needs from Supercube, grouped by topic. It is written so it can be sent to Supercube as it is. Each question says what it affects. When a question is answered, the answer and the date are written next to it.

## 1. Permissions (one signed checklist)

We propose to settle these points on one page that Supercube signs.

- [ ] May MechAi store the Storm handbook on Supercube's server and use it inside the app? (The handbook belongs to OTL Italia.)
- [ ] May the handbook text be sent to the Mistral API (a French AI company with servers in the EU)? Two things are sent: **the full text once per handbook version**, to build the search index (embeddings), and **the matching sections for each question**, to write the answer. Before go-live we check Mistral's API terms on training with our data and switch that off where possible. Until this is signed, we only work with a few test pages.
- [ ] May MechAi connect to Supercube's GraphQL API, both to read kart status and alerts and to mark karts broken or repaired and run diagnostics?
- [ ] May we show a few handbook pages and screenshots of MechAi at school presentations and in the final report?
- [ ] Will Supercube write or approve the fixed safety texts (see section 4)?
- [ ] Should all data be deleted at the end of the project, or does Supercube want to keep MechAi running?

## 2. Server and network

- [ ] Which server will MechAi run on, and what does it run (operating system, Docker, Kubernetes)? MechAi is delivered as Docker containers with a Docker Compose file. Kubernetes files can be added if Supercube's IT uses Kubernetes.
- [ ] Can the server reach the internet for outgoing calls to the Mistral API (`api.mistral.ai`)?
- [ ] Is the customers' guest Wi-Fi a separate network from the internal one?
- [ ] May our documentation, which our teachers read, describe your GraphQL API schema?
- [ ] Who should own the code at the end of the project, and who maintains it afterwards?
- [ ] Which internal hostname can MechAi use, and can Supercube IT provide an HTTPS certificate for it? Installing the app on a tablet, the camera and the microphone only work over HTTPS.
- [ ] Are the workshop tablets and the mechanics' phones on the internal Wi-Fi network?
- [ ] Who sets up the nightly backup of the database and the file folder, and where are backups stored?
- [ ] Would Supercube rather use its own Mistral account (or another AI provider it already has a contract with)? MechAi can switch provider in one place.

## 3. GraphQL API

- [ ] Can MechAi get access to the API? Is there a test environment or recorded sample data?
- [ ] How does a server sign in (API key, service token or another method)?
- [ ] Which WebSocket protocol do the subscriptions use (`graphql-transport-ws` or the older `subscriptions-transport-ws`)?
- [ ] What do the alert codes mean? Are they the controller failure codes from handbook section 6.2.1 (pages 55-56), or Supercube's own codes? Is there a list?
- [ ] How does a pod id map to the number on the kart (for example kart 07)?
- [ ] Are times in UTC?
- [ ] Diagnostics: does the operator app show the same speed modes as the API (the schema also has SAFETY and SLOW)? MechAi will show Pitlane, Cruise, Boost, High boost and High brake, like the operator app.

## 4. Safety

- [ ] What is Supercube's procedure for high-voltage and battery work, and for emergencies (smoke, fire, a swollen or hot battery, someone hurt)? MechAi shows these texts word for word and never lets the AI write these steps.
- [ ] Who is qualified for which electrical task (in Belgium often BA4 or BA5)? This is Supercube's decision; MechAi only shows it.
- [ ] Which senior mechanic can review the safety questions and answers before the final presentation?
- [ ] Who should be alerted when a kart is reported unsafe: all seniors, or only the senior on shift?

## 5. Documents and data

- [ ] Which revision of the Storm handbook is current? The file name says V13, the page footer says rev 12 (01-08-2017).
- [ ] Is there documentation for Supercube's own AR parts (headset, the PC in the steering wheel, the network switch)? They are not in the OTL handbook.
- [ ] Are there wiring diagrams beyond the handbook (pages 81-89), and do they have written pin tables?
- [ ] Is there an existing repair history (paper, spreadsheet, software) that can be imported?
- [ ] How is stock tracked today, and is there a parts list with part numbers and shelf locations?
- [ ] Are there CAD files of the kart? They would make an accurate 3D view possible.
- [ ] What may appear in photos (people, customers, venue details)? Our proposal is: never photograph people.

## 6. Later

- [ ] Does Supercube want MechAi integrated into its own systems later, for example behind the login of the operator app? The login code sits in one module, so this is possible.
