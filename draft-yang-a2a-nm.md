---
title: "A2A"
category: info

docname: draft-yang-a2a-nm-latest
submissiontype: IETF  # also: "independent", "editorial", "IAB", or "IRTF"
number:
date:
consensus: true
v: 3
# area: AREA
# workgroup: WG Working Group
keyword:
 - next generation
 - unicorn
 - sparkling distributed ledger
venue:
#  group: WG
#  type: Working Group
#  mail: WG@example.com
#  arch: https://example.com/WG
  github: "Yuanyuan4666/A2A"
  latest: "https://Yuanyuan4666.github.io/A2A/draft-yang-a2a-nm.html"

author:
 -
    fullname: "Yuanyuan4666"
    organization: Your Organization Here
    email: "yangyuanyuan55@huawei.com"

normative:

informative:


--- abstract

TODO Abstract


--- middle

# Introduction

With the advancement of large language models (LLMs), the concept of AI agents has gradually attracted significant attention. An AI agent refers to a category of software applications that utilizes LLMs to interact with users or other agents and accomplish specific tasks. Some examples of AI agents are:

- A fitness AI agent that recommends suitable physical activities for users based on users' health conditions, geographical locations, weather, and wind factors.
- A multimodal AI agent that collaborates with domain-specific agents to complete diverse tasks such as translation, image generation, and video production."

Fundamentally, an AI agent is developed based on large language models (LLMs), with its prompt engineering varying according to its specialized domain. Sophisticated prompts typically incorporate:

- Domain-specific documentation
- Available tools and capabilities
- Function callings (in some cases)
- User-provided inputs

Based on this comprehensive prompt structure, the LLM dynamically determines subsequent actions, which may involve continuing dialogue with users to gather additional information, invoking appropriate tools to execute specific functions, or initiating interactions with other specialized agents.

The aforementioned examples demonstrate that AI agents are typically domain-specific, which raises an important challenge: users may request an agent to perform tasks beyond its specialized capabilities. In such cases, a more effective solution involves enabling the current agent to communicate with other agents and delegate tasks to better-suited counterparts.


# Conventions and Definitions

- AI Agent: A software system or program that is capable of autonomously performing goals and tasks on behalf of a user or another system.
- Agent Card: A common metadata file that describes an agent's capabilities, skills, interface URLs, and authentication requirements. Clients discover and identify the agent through this file.
- A2A server: An AI agent that receives requests and performs tasks
- A2A client: An AI agent that sends requests to servers

# Overview of key challenges for the network management

In large scale network management environment, a large number of devices from different vendors need to be uniformly managed, which can lead to the following issues:

## Limitations of Unified AI Agents in Heterogeneous NETCONF/YANG Environments

Vendor implementations of YANG models and NETCONF/RESTCONF protocols exhibit significant divergence. A unified AI agent trained with homogeneous datasets and operating within fixed contextual frameworks inherently fails to adapt to vendor-specific device behaviors, resulting in suboptimal management performance, primarily due to:

- **Overgeneralized Training Data**: Single training corpus cannot capture all vendor implementations

- **Inflexible Contextual Frameworks**: Static operational contexts cannot accommodate device-specific nuances

## Operational Inefficiencies in Multi-Device Management Scenarios

In multi-device operational environments, critical workflows including:

- Fault diagnosis
- Traffic monitoring
- Security enforcement

often require engineers to:

- Manually collect and correlate logs across devices
- Perform root cause analysis without cross-device context
- Validate solutions through iterative device-by-device testing
- Act as human intermediaries for inter-device communication

This approach introduces significant operational inefficiencies and suboptimal human resource utilization.

# Operational Consideration

# Conclusion

# Security Considerations

TODO Security


# IANA Considerations

This document has no IANA actions.


--- back

# Reference

TODO acknowledge.
