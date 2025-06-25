---
title: "Applicability of A2A to the Network Management "
category: info

docname: draft-yang-a2a-nm-latest
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
    fullname: Yuanyuan Yang
    organization: Huawei
    email: "yangyuanyuan55@huawei.com"
 -
   fullname: Qin Wu
   organization: Huawei
   email: bill.wu@huawei.com
 -
   fullname: Houda Chihi
   organization: InnovCOM Sup'COM
   email: houda.chihi@supcom.tn
 -
  fullname: Diego Lopez
  organization: Telefonica
  email: diego.r.lopez@telefonica.com
 -
  fullname: Nathalie Romo Moreno
  organization: Deutsche Telekom
  email: nathalie.romo-moreno@telekom.de

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

Agent to Agent Communication protocol(A2A) provides a standardized way for AI agents to communicate and collaborate across different platforms and frameworks through a structured
process, regardless of their underlying technologies. Agents can advertise their capabilities using an 'Agent Card' in JSON format, or send
messages to communicate context, replies, artifacts, or user instructions, which make it easier to build AI applications that can interact
with heterogeneous AI ecosystems in specific domain.

With significant adoption of AI Agents across the Internet, A2A may become the foundation for the next wave of Internet communication technologies across domains {{?I-D.rosenberg-ai-protocols}}. The application of A2A in the network management field aims to develop various AI-driven network applications and realize intent-based network management automation in multi-vendor heterogeneous network environments.

To achieve this vision, A2A establishes standard interfaces that address key challenges in multi-agent collaboration. First, it provides dynamic capability discovery mechanisms that allow agents to automatically identify and understand what services other agents can provide, eliminating the need for static configuration. Second, it enables intelligent message routing that can direct communications between agents based on their capabilities and current availability, ensuring efficient collaboration. Finally, it enables cross-platform interoperability by providing common protocols that allow agents to collaborate seamlessly across different AI frameworks, platforms, and implementation approaches, abstracting away underlying technical differences.

This document discusses the applicability of A2A to the network management
in the multi-domain heterogeneous network environment that utilizes IETF technologies. It explores operational
aspect, key components, generic workflow and deployment scenarios. The impact
of integrating A2A into the network management system is also discussed.


# Conventions and Definitions

- AI Agent: A software system or program that is capable of autonomously performing goals and tasks on behalf of a user or another system.
- Agent Card: A common metadata file that describes an agent's capabilities, skills, interface URLs, and authentication requirements. Clients
              discover and identify the agent through this file.
- A2A Server: An AI agent that receives requests and performs tasks
- A2A Client: An AI agent that sends requests to servers

# Overview of key challenges for the network management

In large scale network management environment, a large number of devices from different network vendors need to be uniformly managed, especially in the
heterogeneous network environment which can lead to the following issues:

## Protocol and Data Model Fragmentation in Multi-Vendor Networks

In the multi-vendor heterogeneous environment,vendors implementations of YANG models and NETCONF/RESTCONF protocols {{!RFC6241}}{{!RFC8040}} exhibit
significant divergence. Different vendors implement different YANG models such as IETF YANG, Openconfig YANG, Vendor specific YANG. Some vendors only
partially support standard Network management protocols while Other vendors might choose non-stanard network management protocol or telemetry protocol
such as gnmi {{?I-D.openconfig-rtgwg-gnmi-spec}}, grpc {{?I-D.kumar-rtgwg-grpc-protocol}}. Without standard protocol or open programmable framework with
multi-vendors integration drivers, integration various different data models and management protocols and allowing quickly adapt to different device are
still big challenges. The same challenge is applied to multi-domain heterogeneous environment.

## Inflexibility of Static Data Models for Evolving Service Requirements

While YANG models provide a structured approach to network service configuration, their static nature creates significant bottlenecks in rapidly evolving service environments. YANG models are typically defined during the design phase with fixed schemas that specify predetermined attributes and capabilities. When new service requirements emerge—such as novel QoS parameters, security features, or performance metrics—the existing YANG models cannot dynamically accommodate these additions.

For example, if a network operator wants to introduce machine learning-based traffic optimization as a new service feature, the current YANG model may lack the necessary attributes to configure or monitor this capability. Adding these attributes requires updating the YANG schema, going through standardization processes, and potentially coordinating across multiple vendors—a process that can take months or years. This rigidity prevents network operators from quickly deploying innovative services and limits their ability to respond to changing market demands or customer requirements.

The static nature of current data models thus creates a fundamental mismatch between the pace of service innovation and the flexibility of management interfaces.

## YANG Model Lacks integration with Open APIs

Today, Open API has been widely adopted by the northbound interface of OSS/BSS or Network orchestrator while YANG data models have been widely adopted by
the northbound interface of the network controller or the southbound interface of the network controller. However Open API ecosystem and
YANG model ecosystem are both built as silo and lack integration or mapping between them.

# Operational Consideration

This section outlines operational aspects of A2A with Network management requirements as follows:

- *Dynamic Capability Discovery and Negotiation*: Agent can automatically detect and understand each other's capabilities, enabling more intelligent and adaptive interactions.

- *Task Management*: The A2A protocol enables agents to coordinate when working together to fulfill user requests. Agents can communicate about their progress and share information needed to complete collaborative work.

- *Automated Workflow Coordination*: Agents can understand high-level user intent and execute complex, multi-step workflows that span multiple agents. This enables intelligent sequencing of network operations, such as coordinating service provisioning across discovery, validation, and configuration phases.

# Architecture Overview

Large language models (LLMs) inherently excel at understanding complex user instructions, a capability that becomes even more pronounced in an AI agent-to-agent (A2A) architecture. Beyond merely comprehending sophisticated requirements, they can autonomously orchestrate lengthy network management workflows, making them particularly suitable for large-scale network management scenarios. Therefore, we have introduced the A2A protocol in the network management environments for building an intelligent network management and control platform.

## Multi-Agent Communication Deployment Scenario
~~~~
                                +-------------+
                                |    User     |
                                +-----+-------+
                                      |
                                +-----+-------+
                              Service Orchestrator
                                | (AI Agent)  |
                                +-----+-------+
                                      |Agent to Agent
                  +-------------------+------------------+
                  |                   |                  |
             +----+-------+     +-----+-------+     +----+------+
           Network Controller  Network Controller  Network Controller
             |(AI Agent)  |     | (AI Agent)  |     |(AI Agent) |
             +----+-------+     +-----+-------+     +----+------+
                  |                   |                  |
                  |                   |                  |
           Agent to tools       Agent to  tools      Agent to tools
                  |                   |                  |
             +----+-------------------+------------------+------+
             |                     Network                      |
             |                     Devices                      |
             +--------------------------------------------------+
~~~~

In the multi-agent communication deployment scenario, AI Agents can be deployed at both service layer and network layer,e.g.,
both service orchestrator and network controller can introduce AI Agent and allow Agent to Agent communication. AI Agent
within the service orchestrator can provide registry database for other service agents within the network controller to
register its location.

The interaction in the multi-agent communication deployment scenario can be break down into:

- *AI Agent to Agent interaction*

- *AI Agent to Tools interaction*

For AI Agent to Tools interaction, to enable comprehensive functionality, additional protocol extensions are required to address two critical aspects:
 (1) standardized tool invocation mechanisms for agent-tool interoperability, and (2) monitoring frameworks for tool usage tracking and auditing.

AI Agent to Agent interaction, users require a real-time monitoring interface for long-running workflows or tasks requiring continuous supervision with dual
capabilities: (1) live network state observation and (2) validation of agent-proposed remediation actions during anomaly resolution scenarios.

A general workflow is as follows:

- User Input Submission: An operator submits a natural language request to a central AI agent.
- Agent Intent Processing: The central AI agent processes natural language inputs by parsing instructions into structured tasks.
- Workflow Graph Decision: The central AI agent decomposing tasks into workflow graphs, and distributes subtasks via an Agent Card Registry to specialized
  subordinate agents based on their capabilities.
- Iteration continues until all tasks reach executable leaf tier agents in the hierarchy.
- Leaf agents report outcomes to the central agent, which dynamically adjusts the workflow based on result analysis and policy rules.

# Impact of integrating A2A on Network Management

## Agent to Agent Interaction

A2A leverages advanced machine learning models or knowledge graph
models and sophisticated communication protocols such as one built
on top of HTTP, SSE, JSON-RPC.

Unlike REST or NETCONF/RESTCONF {{!RFC6241}}{{!RFC8040}}, other open API that follow predefined,
static request-response patterns, A2A introduces a more adaptive communication
model which transforms these interactions into dynamic, context-aware conversations.

In addition, Agents can now negotiate, interpret subtle contextual cues, and make
collaborative decisions in real-time. The cost is more context information needs to
be kept as states in both sides.

## Agent to Tools Interaction

In case of collaboration between small AI model in the network element and large AI model
in the network controller, A2A can be used to negotiate more context related information
and invoke the tools. The cost is more context information needs to be kept as states in
both sides.

In case of no lightweight AI in the network element, REST or NETCONF/RESTCONF, other open API
is sufficient for network management. There is no impact on management protocol used between
the network element and the management system.

If YANG2CLI script has been deployed in the network element, this script can be used to
translate YANG schema into CLI command and mange the 3rd party network device.

# Security Considerations

# IANA Considerations

This document has no IANA actions.


--- back
