KIP-1001: Add CurrentControllerId Metric
================

Created by [Colin
McCabe](https://cwiki.apache.org/confluence/display/~cmccabe), last
modified on [Dec 06,
2023](https://cwiki.apache.org/confluence/pages/diffpagesbyversion.action?pageId=278465658&selectedPageVersions=1&selectedPageVersions=2 "Show changes")

# Status

**Current state**: *adopted*

**Discussion thread**:
[here](https://lists.apache.org/thread/vwtb17sx96q97h882ltck4rrk3w7hrf3)*  
*

**JIRA**:

## [![](https://issues.apache.org/jira/secure/viewavatar?size=xsmall&avatarId=21140&avatarType=issuetype)KAFKA-15980](https://issues.apache.org/jira/browse/KAFKA-15980)

Add KIP-1001 CurrentControllerId metric Resolved

*  
*Please keep the discussion on the mailing list rather than commenting
on the wiki (wiki discussions get unwieldy fast).

# Motivation

The purpose of adding a CurrentControllerId metric is to have an easy
way to identify the current controller by looking at the metrics of any
Kafka node (broker or controller).

# Public Interfaces

### CurrentControllerId

|                                                             |                       |         |              |                                                                   |
|:------------------------------------------------------------|:----------------------|:--------|:-------------|:------------------------------------------------------------------|
| `kafka.server:type=MetadataLoader,name=CurrentControllerId` | Broker and Controller | Integer | KRaft and ZK | Outputs the ID of the current controller, or -1 if none is known. |

The `CurrentControllerId` metric shows the ID of the controller, as seen
by the node in question. If the current node doesn’t think there is an
active controller, the value of thisd metric will be -1.

# Compatibility, Deprecation, and Migration Plan

Since this is a new metric, there are no compatibility issues.

# Test Plan

The new metric will need unit and integration tests as per usual.

# Rejected Alternatives

One rejected alternative is using the existing
`ActiveControllerCount`metric. However, when in KRaft mode,
`ActiveControllerCount` is only exposed on controller nodes, not on
broker nodes. That makes it impossible to monitor what the brokers think
the current active controller is.
