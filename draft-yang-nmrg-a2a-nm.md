---
title: "Applicability of A2A to the Network Management "
category: info

docname: draft-yang-nmrg-a2a-nm-latest
submissiontype: IETF  # also: "independent", "editorial", "IAB", or "IRTF"
number:
date:
consensus: true
v: 3
# area: OPS and ART
# workgroup: Network Working Group
keyword:
 - A2A
 - Network Management

venue:
#  group: WG
#  type: Working Group
#  mail: WG@example.com
#  arch: https://example.com/WG
  github: "Yuanyuan4666/A2A"
  latest: "https://Yuanyuan4666.github.io/A2A/draft-yang-a2a-nm.html"

author:
 -
  fullname: Diego Lopez
  organization: Telefonica
  email: diego.r.lopez@telefonica.com
 -
  fullname: Nathalie Romo Moreno
  organization: Deutsche Telekom
  email: nathalie.romo-moreno@telekom.de
 -
  fullname: Lionel Tailhardat
  organization: Orange ResearchAdd commentMore actions
  email: lionel.tailhardat@orange.com
 -
    fullname: Qiufang Ma
    organization: Huawei
    email: maqiufang1@huawei.com
 -
   fullname: Qin Wu
   organization: Huawei
   email: bill.wu@huawei.com
 -
    fullname: Yuanyuan Yang
    organization: Huawei
    email: yangyuanyuan55@huawei.com
 -
   fullname: Shailesh Prabhu
   organization: Nokia
   email: shailesh.prabhu@nokia.com

contributor:
 -
   fullname: Houda Chihi
   organization: InnovCOM Sup'COM
   email: houda.chihi@supcom.tn

normative:

informative:


--- abstract

This document discusses the applicability of A2A to the network management
in the multi-domain heterogeneous network environment that utilizes IETF technologies. It explores operational
aspect, key components, generic workflow and deployment scenarios. The impact
of integrating A2A into the network management system is also discussed.


--- middle

# Introduction

With the advancement of large language models (LLMs), the concept of AI agents has gradually attracted significant attention. An AI agent
refers to a category of software applications that utilizes LLMs to interact with users or other agents and accomplish specific tasks. Take
a multimodal AI agent as an example, it can collaborate with other domain-specific agents to complete diverse tasks such as translation,
configuration generation, and API development.

A2A provides a standardized way for AI agents to communicate and collaborate across different platforms and frameworks through a structured
process, regardless of their underlying technologies. Agents can advertise their capabilities using an 'Agent Card' in JSON format, or send
messages to communicate context, replies, artifacts, or user instructions, which make it easier to build AI applications that can interact
with heterogeneous AI ecosystems in specific domains.

With significant adoption of AI Agents across the Internet, Agent to Agent Communication protocol may become the foundation for the next wave
of Internet communication technologies across domains {{?I-D.rosenberg-ai-protocols}}. The application of A2A in the network management field
is meant to develop various rich AI driven network applications, realize intent based networks management automation in the multi-vendor
heterogeneous network environment. By establishing standard interfaces for dynamic Capability Discovery, intelligent message routing, heterogeneous
AI ecosystems interaction, cross-platform collaboration, A2A enables AI Agents to:

o Understand contextual nuances

o Negotiate and adapt in real-time

o Make collaborative decisions

o Maintain persistent, intelligent interactions

This document discusses the applicability of A2A to the network management
in the multi-domain heterogeneous network environment that utilizes IETF technologies. It explores operational
aspect, key components, generic workflow and deployment scenarios. The impact
of integrating A2A into the network management system is also discussed.


# Conventions and Definitions

- AI Agent:   A software system or program that is capable of autonomously performing goals and tasks on behalf of a user or another system.
- Agent Card: A common metadata file that describes an agent's capabilities, skills, interface URLs, and authentication requirements. Clients
              discover and identify the agent through this file.
- A2A Server: An AI agent that receives requests and performs tasks
- A2A Client: An AI agent that sends requests to servers

# Overview of key challenges for the network management

As described in {{?I-D.wmz-nmrg-agent-ndt-arch}}, 3 key challenges to apply
A2A protocol to network management have been listed:

o High Risk Operations of Agent2Agent interaction

  * High risk operation can can to large-scale network outages.

o The timeliness requirement of Agent2Agent collaboration

* "Token-based" generation and reasoning approach, limited by computing power and algorithms, result in  slow reasoning speeds.

* Task-oriented "request-response" model without event subscription is unlike to meet time constraints for tasks such as fault
diagnosis, complaint handling, and user experience improvement.

o The Agent2agent Collaboration Reliability

* Incorrect or outdated network configuration data results in incorrect repair advice when diagnosing network incidents or faults.

* Task collaboration is incomplete or not sufficient to handle strategies such as task rejection, missing information during task
collaboration, and failure to achieve task objectives.

# Agent2Agent Architecture Design for Network Management

~~~~

+----------------------------------------------------------------+
| Service Level                                                  |
|  +----------------+  +----------------+   +----------------+   |
|  |Service AI Agent|  |Service AI Agent|   |Service AI Agent|   |
|  +---------+------+  +----------------+   +-------+--------+   |
+------------+--------------------------------------+------------+
             |                                      |
+------------+----------------+ +-------------------+-----------+
|Network Level                | |                   |           |
|            |                | |                   |           |
|    +------------------+     | |     +-------------+------+    |
|    | Network AI Agent |     | |     |  Network AI Agent  |    |
|    +-------+----------+     | |     +---------+----------+    |
|     -+-----+------+-        | |        -+-----+------+        |
|      |            |         | |         |            |        |
|   +--+--+      +--+--+      | |      +-----+      +--+--+     |
|   |Task |      |Task |      | |      |Task |      |Task |     |
|   |Agent|      |Agent| ...  | |      |Agent|      |Agent| ... |
|   +--+--+      +--+--+      | |      +--+--+      +--+--+     |
+------+------------+---------+ +---------+------------+--------+
       |            |                     |            |
       +-----+------------------+-------------------+--+
             |                  |                   |
+------------+------------------+-------------------+-----------+
|Network Element Level:         |                   |           |
|     +------+-------+   +------+-------+    +------+-------+   |
|     | +----+-----+ |   |+------------+|    |+------------+|   |
|     | | NE  Agent| |   ||  NE  Agent ||    ||  NE  Agent ||   |
|     | |  +---+   | |   ||+----------+||    ||+----------+||   |
|     | |  |SLM|   | |   |||MCP Server|||    |||MCP Server|||   |
|     | |  +---+   | |   ||+----------+||    ||+----------+||   |
|     | +----------+ |   |+-----------++|    |+-----------++|   |
|     +--------------+   +--------------+    +--------------+   |
+-------------------  Smart Network Element---------------------+

~~~~

As described in {{?I-D.wmz-nmrg-agent-ndt-arch}}, in the multi-agent communication deployment scenario, AI Agents can be
deployed at both service layer,network layer and Network Element Level, e.g.,
both service orchestrator and network controller can introduce AI Agent and allow Agent to Agent communication. Service
AI Agent within the service orchestrator can provide registration center for other network AI agents and task agents within
the network controller to register its location. In the meanwhile Network AI Agent within the network Controller can
provide registration center for task agents at the network level and Network element level AI agent within the smart network
element.

The interaction in the multi-agent communication deployment scenario can be broken down into:

- *AI Agent to Agent interaction*

- *AI Agent to Tools/APIs/Models interaction*

For AI Agent to Tools/APIs/Models interaction, to enable comprehensive functionality (e.g., large AI model
and small AI model collaboration, network AI agent and Network element AI agent collaboration
for routing protocol troubleshooting), additional protocol extensions are required to address two critical aspects:
 (1) standardized tool invocation mechanisms for agent-tool/api/model interoperability, and (2) monitoring frameworks
 for tool usage tracking and auditing.

AI Agent to Agent interaction, human operators require a real-time monitoring interface for long-running workflows or tasks
requiring continuous supervision with dual capabilities: (1) live network state observation and (2) validation of agent-proposed
remediation actions during anomaly resolution scenarios.

A general workflow is as follows:

- User Input Submission: An operator submits a natural language request to a Service AI agent.

- Agent Intent Processing: The service AI agent processes natural language inputs by parsing instructions into structured tasks.

- Autonomous Close Loop Workflow Management: The service AI agent decomposing tasks into workflow map with subtasks, and
  distributes subtasks via an Agent Card Registry to specialized task agents based on their capabilities.

- Task Execution: Iteration continues until all tasks reach executable task agents in the hierarchy.

- Task Report: Task agents report outcomes to the central agent, which dynamically adjusts the workflow based on result analysis and policy rules.

# Operational Considerations

The introduction of A2A-based agent interactions into network management has several operational implications that MUST be considered when deploying the architecture in large-scale or multi-domain networks. This section highlights key aspects related to performance, scalability, reliability, latency, and agent lifecycle operations.

## Scalability

Large operational networks may contain tens of thousands of devices, multiple administrative domains, and a distributed set of controllers and orchestrators. The use of conversational, context-rich A2A messaging increases message volume compared to static RPC-based interfaces such as NETCONF or RESTCONF.

Operators should evaluate:

- The number of agents required per domain or per function.

- The expected message growth as workflows involve multiple agents performing negotiation, capability discovery, and state exchange.

- The impact of concurrent multi-agent workflows on control-plane stability.

- Whether hierarchical or federated agent structures are needed to avoid message storms and to localize decisions.

Mechanisms for rate-limiting, backoff, and prioritization may be needed to prevent overload.

## Latency and Performance Constraints

Task decomposition and negotiation across multiple agents can introduce non-trivial latency, especially when agents rely on external AI inference engines or large language models (LLMs).

Operational environments may impose strict timing requirements, for example during:

- Service activation with customer-facing SLAs.

- Fault detection and automated remediation loops.

- Real-time telemetry-driven control such as congestion mitigation.

Implementations SHOULD define performance envelopes, including:

- Maximum agent-to-agent message processing latency.

- Timeout and retry behavior for workflow steps.

- Acceptable degradation under load or partial failures.

Fallback mechanisms (e.g., reverting to direct controller APIs or static policies) SHOULD be provided when A2A interactions cannot meet timing constraints.

## Reliability and Failure Handling

A2A workflows may involve long-lived tasks that span multiple agents and systems. Operational networks require predictable and safe behavior under partial failures.

Operators SHOULD consider:

- How workflow state is checkpointed or restored if an agent becomes unreachable.

- How to detect and mitigate inconsistent or stale agent state.

- Whether workflows can be retried idempotently.

- Requirements for transactionality or rollback comparable to NETCONF confirmed-commit semantics.

Implementations SHOULD include mechanisms for workflow monitoring, circuit-breakers, and automatic escalation to human operators in case of sustained failure.

## Agent Lifecycle and Resource Management

Production deployment of A2A-based systems requires active management of agent lifecycles, including:

- Agent onboarding and registration.

- Updates and model re-training (for AI-driven agents).

- Decommissioning and revocation of compromised agents.

- Resource consumption limits for CPU, memory, and inference workloads.

Operators SHOULD maintain visibility into the operational state of all agents and their dependencies, including telemetry on message rates, errors, and workflow completion metrics.

## Inter-Domain Operational Challenges

In multi-domain scenarios (e.g., between business units, operators, or federated networks), operational concerns are amplified due to:

- Differences in local policies or SLAs.

- Variations in controller capabilities and data models.

- Latency and reliability across administrative boundaries.

- Need for shared or interoperable agent capability descriptions.

Standardized operational practices MAY be required for agent discovery, trust establishment, conflict resolution, and accountability.

# Event-driven Agent to Agent Communication

The event-driven Agent to Agent communication enhances the task-based A2A procotol to support proactive and real-time communication based on network events. By leveraging the Message Broker such as Apache Kafka to facilitate the exchange of event messages among different AI agents, it allows the real-time response to maintain network reliability and service assurance in network management and operations. {{event-arch}} gives an overview of the architecure.

~~~~
+---------+                               +----------+
|         |      Agent to Agent           |          |
|AI Agent <-------------------------------> AI Agent |
|         |                               |          |
+---+-----+                               +-----^----+
    |                                           |
    | Events                                    | Events
    |           +----------------+              |
    +----------->Messaging topics|--------------+
                +----------------+
~~~~
{: #event-arch title="An Architecture for Event-driven A2A" artwork-align="center"}

The event-driven extension introduces a publish/subscribe paradigm alongside the primary task-driven interaction. For example, a "Fault Agent" identifies a
link failure by data analyzing and publishes a message to the Message Broker, the "recovery agent" subscribes to the topic and it could initiate a task to generate recovery strategies such as link switching and traffic rerouting and submit to the operator for approval upon consuming the message.

# Security Considerations

The communication between Agents for the exchange of context information, capability information
and user instruction is security sensitive and requires authentication, authorization, and integrity
protection. Legacy communication protocols such as HTTPS/TLS, designed for human-centric interactions,
simply cannot withstand the high-speed exchanges between intelligent agents.  Key security challenges
in AI agent communication include:

- Identity Verification: Ensuring that agents are who they claim to be

- Data Integrity: Preventing unauthorized modifications during transmission

- Confidentiality: Protecting sensitive information from potential breaches

- Scalable Security: Maintaining robust protection across diverse and complex networks


# IANA Considerations

This document has no IANA actions.


--- back

# Usage Example

This section describes the deployment of a network configuration within a secure video meeting context.
The scheduling agent is deployed to the Service Orchestrator, while the worker agent is deployed to the
network controller. Registered on the Service Orchestrator, the agent card formally defines a worker
agent's capabilities, interfaces, and operational characteristics within network management systems.

See the following Agent card examples for two worker agents (QoS Agent and Security Agent):

~~~~
# Worker Agents Capabilities
{
    "name": "QoSAgent",
    "description": "Automatically configure QoS policies",
    "url": "https://qos-agent.example.com/tasks/send",
    "capabilities": ["QoS_Policy"],
    "skills": [
        {
            "id": "set_qos",
            "name": "QoS configuration",
            "description": "QoS configuration",
            "inputModes": ["text/structured"],
            "outputModes": ["text/status"]
        }
    ]
}
{
    "name": "SecurityAgent",
    "description": "Automatically configure network security policies",
    "url": "https://security-agent.example.com/tasks/send",
    "capabilities": ["IPSEC", "DTLS"],
    "skills": [
        {
            "id": "enable_encryption",
            "name": "Encryption method configuration",
            "description": "Encryption method configuration",
            "inputModes": ["text/structured"],
            "outputModes": ["text/status"]
        }
    ]
}
~~~~

Suppose a user submits a natural language request such as "The meeting will have 100 participants. The security level is Top Secret" to the platform integrated with the Service Orchestrator. The platform parses the request and converts it into JSON format as follows:

~~~~
# Requested Service Configuration
{
    "taskId": "task-multi-001",
    "action": "deploy_network_configuration",
    "parameters": {
        "context": "secure_video_meeting",
        "scope": "100",
        "secure_level": "Top Secret",
    }
}
~~~~

The Service Orchestrator sends subtasks in a structured format to the Network Controller. For example, the subtasks for `set_qos` and `enable_encryption` are structured as follows:

~~~~
# Set QoS and Enable Encryption Subtasks
{
    "taskId": "task-multi-001",
    "subTasks": [
        {
            "agent": "QoSAgent",
            "action": "set_qos",
            "parameters": {
	            "configuration": {
		            "acceptedOutputModes": [
			            "text/status"
                    ]
	            },
	            "minimum_bandwidth": "100Mbps",
	            "priority": "0"
            }
        },
        {
            "agent": "SecurityAgent",
            "action": "enable_encryption",
            "parameters": {
	            "configuration": {
		            "acceptedOutputModes": [
			            "text/status"
                    ]
	            },
	            "encryption_method": "ipsec",
	            "key_management": "dtls",
            }
        }
    ]
}
~~~~

The network controller executes network management operations on network devices and returns the results to the Service Orchestrator in JSON format. Example responses for the subtasks are shown below:

~~~~
# Network Configuration Feedback Results
{
    "taskId": "task-multi-001",
    "action": "deploy_network_configuration",
    "parameters": {
        "context": "secure_video_meeting",
        "scope": "100",
        "secure_level": "Top Secret",
    }
}
{
  "taskId": "subtask-qos-001",
  "status": "completed",
  "artifacts": [{"type": "text", "content": "QoS setup completed"}]
}
{
  "taskId": "subtask-sec-001",
  "status": "completed",
  "artifacts": [{"type": "text", "content": "IPSEC encryption enabled"}]
}
~~~~
