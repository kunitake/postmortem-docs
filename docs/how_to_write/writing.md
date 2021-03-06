---
cover: assets/img/covers/post-mortem_process.png
description: Here are concrete steps for producing a postmortem document. You will learn the most important information to include in the postmortem, how to collect and present that information, and how to conduct an effective analysis that results in system improvements.
---
![Step by Step](../assets/img/headers/step_by_step.png)

Below are the steps involved in performing a postmortem at a high level. Below are the details of how to perform each step.

1. Create a new postmortem for the incident.
2. Schedule a postmortem meeting within the required timeframe for all required and optional attendees on the "Incident Postmortem Meetings" shared calendar.
3. Populate the incident timeline with important changes in status/impact and key actions taken by responders.
    * For each item in the timeline, include a metric or some third-party page where the data came from.
4. Analyze the incident.
    * Identify superficial and root causes.
    * Consider technology and process.
5. Open any follow-up action tickets.
6. Write the external messaging.
7. Ask for review.
8. Attend the postmortem meeting.
9. Share the postmortem.

## Owner Responsibilities
At the end of a major incident call, or very shortly after, the [Incident Commander](https://response.pagerduty.com/training/incident_commander/) selects one responder to own the postmortem. The selected owner will be notified directly by the Incident Commander. Writing the postmortem will ultimately be a collaborative effort, but selecting a single owner will help ensure it gets done.

As owner of a postmortem, you are responsible for the following:

* Scheduling the postmortem meeting on the shared calendar and inviting the relevant people (this should be scheduled within 3 calendar days for a Sev-1 and 5 business days for a Sev-2).
* Investigating the incident, pulling in whomever you need from other teams to assist in the investigation.
* Ensuring the page is updated with all of the necessary content. See our [Template](../resources/post_mortem_template.md) for what should be included.
* Creating follow-up tickets. (You are only responsible for creating the tickets, not following them up to resolution).
* Reviewing the postmortem content with appropriate parties before the meeting.
Running through the topics at the postmortem meeting (the Incident Commander will "run" the meeting and keep the discussion on track, but you will likely be doing most of the talking).
* Communicating the results of the postmortem internally.

After you are designated as the owner of a postmortem, create the postmortem document and start updating it with all relevant information.

## Administration
![Administration](../assets/img/thumbnails/1Administration.png)
1. Create the document.
2. Add all responders to it.
3. Schedule the meeting.

If not already done by the Incident Commander, your first step is to create a new, empty postmortem for the Incident. Go through the history in Slack to identify the responders and add them to the page so they can help populate the postmortem. Include the Incident Commander and Scribe as well. Add a link to the incident call recording.

Next, schedule the postmortem meeting for 30 minutes to an hour, depending on complexity of the incident. Scheduling the meeting at the beginning of the process helps ensure the postmortem is completed within the SLA. **The meeting should be scheduled within 3 calendar days for a Sev-1 and 5 business days for a Sev-2.** Don’t worry about finding the best time for all attendees. Your priority is to schedule within this timeframe and attendees should adjust their schedules accordingly. We schedule all postmortem meetings on a shared “Incident Postmortem Meetings” calendar so they are easily discoverable for any interested parties across the organization.

Invite the following people to the postmortem meeting:

* Always
    * The [incident commander](https://response.pagerduty.com/training/incident_commander/).
    * The incident commander shadowee (if there was one).
    * [Service owners](https://response.pagerduty.com/training/subject_matter_expert/) involved in the incident.
    * Key engineer(s)/responders involved in the incident.
    * Engineering manager for impacted systems.
    * Product manager for impacted systems.
* Optional
    * [Customer liaison](https://response.pagerduty.com/training/customer_liaison/) (only for Sev-1 incidents).

PagerDuty postmortems have a "Status" field that indicates where in our process the postmortem currently is. Here's a description of the values and how we use them.

| Status | Description |
|-|-|
| **Draft** | Indicates that the content of the post-mortem is still being worked on. |
| **In Review** | The content of the post-mortem has been completed, and is ready to be reviewed during the post-mortem meeting. |
| **Reviewed** | The meeting is over and the content has been reviewed and agreed upon.<br/>If there is an "External Message", the Customer Support team will take the message and update our status page as appropriate. |
| **Closed** | No further actions are needed on the post-mortem (outstanding issues are tracked in JIRA).<br/>If no "External Message", you can skip straight to this once the meeting is over.<br/>If there's an "External Message", then the Support team will update it to this status once the message is posted. |

## Create a Timeline
![Timeline](../assets/img/thumbnails/2CreateATimeline.png)
Begin by focusing on the timeline. Document the facts of what happened during the incident. Avoid evaluating what should or should not have been done and coming to conclusions about what caused the incident. Presenting only the facts here will help avoid blame and supports a deeper analysis. Note the incident may have started before responders became aware of it and began the response effort. The timeline includes important changes in status/impact and key actions taken by responders. To avoid hindsight bias, start your timeline at a point before the incident and work your way forward instead of backwards from resolution.

Review the incident log in Slack to find key decisions made and actions taken during the response effort. Also include information the team didn’t know during the incident that, in hindsight, you wish you would have. Find this additional information by looking at monitoring, logs, and deployments related to the affected services. You’ll take a deeper look at monitoring during the analysis step, but start here by adding key events related to the incident, and include changes to incident status and the impact to the timeline.

For each item in the timeline, identify a metric or some third-party page where the data came from. This helps illustrate each point clearly and ensures you remain rooted in fact rather than opinions. This could be a link to a monitoring graph, a log search, a tweet, etc.—anything that shows the data point you're trying to illustrate in the timeline.

!!! info "Key Takeaways"
    * Stick to the facts.
    * Include changes to incident status and impact.
    * Include key decisions and actions taken by responders.
    * Illustrate each point with a metric.

## Document Impact
![Impact](../assets/img/thumbnails/3DocumentImpact.png)
Impact should be described from a few perspectives:

- **How long was the impact visible? In other words, what was the length of time users/customers were affected?**
    - Note the length of impact may differ from the length of the response effort. Impact may have started some time before it was detected and incident response began.
- **How many customers were affected?**
    - Support may need a list of all affected customers so they can reach out individually.
- **How many customers wrote or called support about the incident?**
- **What functionality was affected and how severely?**
    - Quantify impact with a business metric specific to your product. For PagerDuty this includes event submission, delayed processing, slow notification delivery, etc.

## Analyze the Incident
![Analyze](../assets/img/thumbnails/4AnalyzeTheIncident.png)
Now that you have an understanding of what happened during the incident, look further back in time to find the contributing factors that led to the incident. Technology is a complex system with a network of relationships (organizational, human, technical) that is continuously changing.

In his paper, “[How Complex Systems Fail](http://web.mit.edu/2.75/resources/random/How%20Complex%20Systems%20Fail.pdf),” Dr. Richard Cook says that because complex systems are heavily defended against failure, it is a unique combination of apparently innocuous failures that join to create catastrophic failure. Furthermore, because overt failure requires multiple faults, attributing a “root cause” is fundamentally wrong. **There is no single root cause of major failure in complex systems, but a combination of contributing factors that together lead to failure.** Your goal in analyzing the incident is not to identify the root cause, but to understand the multiple factors that created an environment where this failure became possible.

Cook also says the effort to find the “root cause” does not reflect an understanding of the system, but rather the cultural need to blame specific, localized forces for events. Blamelessness is essential for an effective postmortem. **An individual’s action should never be considered a root cause.** Effective analysis goes deeper than human action. In the cases where someone’s mistake did contribute to a failure, it is worth anonymizing this in your analysis to avoid attaching blame to any individual. Assume any team member could have made the same mistake. According to Cook, “all practitioner actions are actually gambles, that is, acts that take place in the face of uncertain outcomes.”

Start your analysis by looking at your monitoring for the affected services. Search for irregularities like sudden spikes or flatlining when the incident began and leading up to the incident. Include any commands or queries you use to look up data, graph images, or links from your monitoring tooling alongside this analysis so others can see how the data was gathered. If you do not have monitoring for this service or behavior, make building monitoring an action item for this postmortem. More on [writing action items](#followup) below.

!!!  warming "Importance of Monitoring"
    Puppet’s 2018 State of DevOps Report highlights making monitoring configurable by the team operating the service as a foundational practice for successful DevOps. Empowering teams to define, manage, and share their own measurement of performance contributes to a culture of continuous improvement.

Another helpful strategy for targeting what caused an incident is reproducing it in a non-production environment. Experiment by modifying variables to isolate the phenomenon. If you modify or remove some input does the incident still occur?

This level of analysis will uncover the superficial causes of the incident. Next, ask why the system was designed in a way to make this possible. Why did those design decisions seem to be the best decisions at the time? Answering these questions will help you uncover root causes.

Here are some questions to help you identify the class of a particular problem:

- Is it an isolated incident or part of a trend?
- Was this a specific bug, a failure in a class of problem we anticipated, or did it uncover a class of issue we did not architecturally anticipate?
- Was there work the team chose not to do in the past that contributed to this incident?
- Research if there were any similar or related incidents in the past. Does this incident demonstrate a larger trend in your system?
- Will this class of issue get worse/more likely as you continue to grow and scale the use of the service?

!!! tip
    We have a separate process for analyzing larger trends across multiple incidents to inform technical and organizational planning. Learn more in our guide on [Operational Reviews](http://reviews.pagerduty.com).

Though it may not be a root cause, consider process in your analysis. Did the way that people collaborate, communicate, and/or review work contribute to the incident? This is also an opportunity to evaluate and improve your incident response process. Consider what worked well and didn’t work well within your incident response process during the incident.

Write a summary of your findings in the postmortem. You may find further learnings and identify additional causes through discussion in the meeting, but you want to do as much pre-work and documentation as possible to ensure a productive discussion.  

### Questions to Ask
Inspired by Gary Klein’s debriefing questions in Sidney Dekker’s *The Field Guide To Understanding Human Error*, below is a non-exhaustive list to help stimulate deep analysis. Ask “how” and “what” questions, rather than “who” or “why,” to discourage blame and encourage learning.  

<table>
    <tr>
        <td>Cues</td>
        <td>
            <ul>
                <li>What were you focusing on?</li>
                <li>What was not noticed?</li>
                <li>What differed from what was expected?</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td>Previous Knowledge/Experience</td>
        <td>
            <ul>
                <li>Was this an anticipated class of problem or did it uncover a class of issue that was not architecturally anticipated?</li>
                <li>What expectations did participants have about how things were going to develop?</li>
                <li>Were there similar incidents in the past?</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td>Goals</td>
        <td>
            <ul>
                <li>What goals governed your actions at the time?</li>
                <li>How did time pressure or other limitations influence choices?</li>
                <li>Was there work the team chose not to do in the past that could have prevented or mitigated this incident?</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td>Assessment</td>
        <td>
            <ul>
                <li>What mistakes (for example, in interpretation) were likely?</li>
                <li>How did you view the health of the services involved prior to the incident?</li>
                <li>Did this incident teach you something that should change views about this service’s health?</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td>Taking Action</td>
        <td>
            <ul>
                <li>How did you judge you could influence the course of events?</li>
                <li>What options were taken to influence the course of events? How did you determine that these were the best options at the time?</li>
                <li>How did other influences (operational or organizational) help determine how you interpreted the situation and how you acted?</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td>Help</td>
        <td>
            <ul>
                <li>Did you ask anyone for help?</li>
                <li>What signal brought you to ask for support?</li>
                <li>Were you able to contact the people you needed to contact?</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td>Process</td>
        <td>
            <ul>
                <li>Did the way that people collaborate, communicate, and/or review work contribute to the incident?</li>
                <li>What worked well in your incident response process and what did not work well?</li>
            </ul>
        </td>
    </tr>
</table>

!!! info "Key Takeaways"
    * Find contributing factors, not the root cause.
    * Focus on the system, not the humans.
    * Look for anomalies in monitoring.
    * Reproduce and experiment in a non-production environment.
    * Don’t forget to review your processes.

## Follow-Up Actions<a name="followup"></a>
![Followup](../assets/img/thumbnails/5FollowUpActions.png)
After identifying what caused the incident, ask what needs to be done to prevent this from happening again. Based on your analysis, you may also have proposals to reduce the occurrence of this class of problem, rather than this specific incident from recurring.

It may not be possible (or worth the effort) to completely eliminate the possibility of this same incident or a similar incident from happening again, so also consider how you can improve detection and mitigation of future incidents. Do you need better monitoring and alerting around this class of problem so you can respond faster in the future? If this class of incident does happen again, how can you decrease the severity or duration? Remember to identify any actions that can make your incident response process better, too. Go through the incident history in Slack to find any to-do items raised during the incident and make sure these are documented as tickets as well. (At this phase, you are only opening tickets. There is no expectation that tasks will be completed before the postmortem meeting.)

Create tickets for all proposed follow-up actions in your task management tool. Label all tickets with their severity level and date tags so they can be easily found and reported in the ticketing system. Provide as much context and proposed direction on the tickets as you can so the team’s product owner will have enough information to prioritize the task against other work and the eventual assignee will have enough information to complete the task.

In the *;login:* magazine article, “[Postmortem Action Items: Plan the Work and Work the Plan](https://www.usenix.org/system/files/login/articles/login_spring17_09_lunney.pdf),” John Lunney, Sue Lueder, and Betsy Beyer write about how Google writes postmortem action items to ensure they are completed quickly and easily. They advise all action items to be written as actionable, specific, and bounded.

- **Actionable:** Phrase each action item as a sentence starting with a verb. The action should result in a useful outcome.
- **Specific:** Define each action item’s scope as narrowly as possible, making clear what is in and out of scope.
- **Bounded:** Word each action item to indicate how to tell when it is finished, as opposed to open-ended or ongoing tasks.

| Poorly Worded | Better |
|-|-|
| Investigate monitoring for this scenario. | **Actionable:** Add alerting for all cases where this service returns >1% errors. |
| Fix the issue that caused the outage. | **Specific:** Handle invalid postal code in user address form input safely. |
| Make sure engineer checks that database schema can be parsed before updating. | **Bounded:** Add automated presubmit check for schema changes. |

Source: *;login:*  Spring 2017 Vol. 42, No. 1.

If there are any proposed follow-up actions that need discussion before tickets can be created, make a note to add these items to the postmortem meeting agenda. These may be proposals that need team validation or clarification. Discussing these items in the meeting will help decide how best to proceed.

Be careful with creating too many tickets. Only create tickets that are P0/P1's; i.e., tasks that absolutely should be dealt with. There will be some trade-offs here, and that's fine. Sometimes the ROI isn't worth the effort that would go into performing an action that may reduce the recurrence of the incident. When that is the case, it is worth documenting that decision in the postmortem. Understanding why the team is choosing not to perform an action helps avoid learned helplessness.

Note the person who creates the ticket is not responsible for completing it. Tickets are opened under the projects for the teams that own the affected service. At least one representative for all teams that will be responsible for a follow-up action are invited to the postmortem meeting.

!!! info "Key Takeaways"
    * What needs to be done to reduce the likelihood of this, or a similar, incident from happening again?
    * How can you detect this type of incident sooner?
    * How can you decrease the severity or duration of this type of incident?
    * Write actionable, specific, and bounded tasks.

## Write External Messaging
![External](../assets/img/thumbnails/6WriteExternalMessaging.png)
The goal of external messaging is to build trust by giving customers enough information about what happened and what you’re doing about it, without giving away proprietary information about your technology and organization. There are parts of your internal analysis that primarily benefit the internal audience and do not need to be included in your external postmortem.

The external postmortem is a summarized and sanitized version of the information used for the internal postmortem. External postmortems include these three sections:

1. **Summary:** Two to three sentences that summarize the duration of the incident and the observable customer impact.
1. **What Happened:**
    Summary of cause(s).
    Summary of customer-facing impact during the incident.
    Summary of mitigation efforts during the incident.
1. **What Are We Doing About This:** Summary of action items.

>Tip: Avoid using the word "outage" unless it really was a full outage—use the word "incident" or "service degradation" instead. Customers generally see "outage" and assume the worst.

Note that at this point, the external postmortem is drafted language that should not yet be sent. It needs to be reviewed during the postmortem meeting before being sent out.

## Postmortem Review
![Review](../assets/img/thumbnails/7PostmortemReview.png)
At PagerDuty, we have a community of experienced postmortem writers available to review postmortems for style and content. This avoids wasted time during the meeting. We post a link to the postmortem into Slack to receive feedback at least 24 hours before the meeting is scheduled.

Here are some of the things we look for:

* Does it provide enough detail?
* Rather than just pointing out what went wrong, does it drill down to the underlying causes of the issue?
* Does it separate “What happened?” from “How to fix it”?
* Do the proposed action items make sense? Are they well-scoped enough?
* Is the postmortem well-written and understandable?
* Does the external message resonate well with customers or is it likely to cause outrage?

Reviewing a postmortem isn't about nitpicking typos (but do make sure the external message isn't littered with spelling and grammatical errors). It's about providing constructive feedback on valuable changes to a postmortem to get the most benefit from them.
