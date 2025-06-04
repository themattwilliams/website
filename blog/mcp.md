---
template: '../@theme/templates/BlogPost'
title: "MCP: what it is, why it matters, and why caution is warranted in 2025"
description: Explore the pros and cons of Model Context Protocol (MCP), an emerging standard for AI agent interaction.
seo:
  title: "MCP: what is it, why it matters, and why caution is warranted in 2025"
  description: Explore the pros and cons of Model Context Protocol (MCP), an emerging standard for AI agent interaction.
author: 
date: 
categories:
  - mcp
image:
---

# MCP: What It Is, Why It Matters — and Why Caution Is Warranted

In late 2024, Anthropic introduced the **Model Context Protocol (MCP)** — a new way for AI agents to interact with tools and data through standardized interfaces.

MCP has generated excitement across developer communities, especially for its promise to streamline how agents connect to external services.

But it’s also sparked debate, including among API experts and platform engineers, about whether it’s mature or secure enough for wide adoption.

In this post, we’ll explain what MCP does, where it’s useful, and where it falls short — especially for developers trying to build reliable, secure, AI-connected systems.

---

## What MCP is solving for

Today’s AI agents are limited by how they interact with APIs and external tools.

Most integrations require custom code, brittle scripts, or predefined workflows.

MCP proposes a general-purpose solution: a protocol that allows AI agents to “discover and invoke” tools exposed via a consistent JSON interface.

In theory, MCP makes it easier to:

- Expose internal tools to agents without custom wrappers  
- Standardize how agents interact with APIs or file systems  
- Create agent workflows that chain together multiple tools  

This could reduce integration overhead and allow developers to plug new tools into agent systems more quickly.

## What's inside MCP?

At its core, MCP follows a **client-server architecture**:

- The **MCP client**, often embedded inside the AI agent, sends requests.  
- The **MCP server** exposes tools or APIs in a consistent, machine-readable way.  
- Communication happens over **JSON-RPC 2.0**, with calls like `read_file`, `run_tool`, etc.

It’s **model-agnostic** and **open-source**, which makes it appealing to AI platforms trying to standardize their tool interface layer.

## The real-world reality of MCP

Despite the appealing goals, some in the developer and API ecosystem remain cautious — and for good reason.

### 1. Loose Specification

MCP isn’t a formal protocol spec in the traditional sense.

Much of it lives in example code or GitHub discussions, which leads to confusion about implementation details.

There’s no governing body or RFC-like process defining behavior across edge cases.

In its current state, it reads less like a protocol specification and more like a set of conventions.

### 2. Overly Broad Permissions & Security Risks

One major concern came to light in a [recent GitHub issue](https://github.com/modelcontext/protocol/issues/18),
where a misconfigured MCP server exposed internal tools to broader access than intended.

This wasn’t classic prompt injection — it was a permissions scope issue that stemmed from how tools were described and invoked by agents.

Developers rushing to add MCP to their systems often don’t fully isolate or sandbox access.

This creates a real risk, especially when AI agents are granted open-ended access to internal operations.

### 3. Questionable Usefulness for Many Cases

In practice, over half of MCP tools today just expose documentation or basic static data.

Some experts argue that simpler alternatives already exist:

- **Direct HTML parsing** by LLMs  
- **LLMs.txt** (a markdown-based context file format)  
- **OpenAPI + cURL** for structured endpoint interaction  

These approaches are often more efficient and require fewer moving parts.

## What we're keeping an eye on with MCP

We expect more innovation to happen in this space, and we're keeping a close eye on it.
Here's what's most interesting to us today:

- **Enterprise automation**, where internal tools are otherwise hard to expose via APIs  
- **AI-assisted coding**, where context-aware tools can be dynamically invoked  
- **AI agent frameworks and low-code agent builders**, like [Mastra](https://mastra.ai/blog/mastra-mcp)
 and [Gumloop](https://www.gumloop.com/blog/announcing-gumcp) where support of MCP is enabling faster, 
more dynamic agent-powered applications.
- **Additional emerging protocols**, like CopilotKit's [AG-UI](https://github.com/ag-ui-protocol/ag-ui) for
making user-agent interaction more accessible for the frontend, and
[Google's A2A protocol](https://developers.googleblog.com/en/a2a-a-new-era-of-agent-interoperability/)
for agents interacting with other agents.

## Should you use MCP today?

We're hopeful to see MCP and other emerging protcols continue to mature as they're more widely adopted. 

And all things considered, if you're a developer working on AI agent infrastructure, MCP is promising.

As with any emerging technology, spec, or protocol, it’s important to treat it with an **experimental** 
mindset.

MCP is still evolving, security practices are immature, and real-world value is still being proven
out at meaningful scale.

In our view, MCP needs more of the rigor we've been applying to API specs and standards over the 
last two decades.

Before adopting it, we recommend developers:

- **Read the full spec** ([modelcontextprotocol.io](https://modelcontextprotocol.io))  
- **Review security boundaries carefully**  
- **Don’t expose sensitive tools without strict permission controls**  
- **Consider if OpenAPI or direct integrations would suffice**

---

## Final thoughts

MCP is an ambitious attempt to rethink how AI agents interact with the world — and that’s worth exploring.

But right now, it’s better viewed as an **experimental playground** than a production-ready protocol.

We encourage developers to test, share feedback, and improve the ecosystem — but go in with eyes open.

---

## FAQ

**How is MCP different from OpenAPI?**  
MCP is runtime-focused — agents call tools dynamically. OpenAPI is more declarative and often used to generate client libraries or documentation. 
The two can complement each other.

**Is MCP secure?**  
It depends heavily on how it’s implemented. The protocol itself doesn’t enforce access control — that’s up to the developer.

**What happened with the GitHub security issue?**  
A [reported case](https://github.com/modelcontext/protocol/issues/18) showed that an MCP server granted broader access than intended.  
The root issue was a lack of scoped permissions in how tools were defined and invoked.

**Is MCP necessary?**  
Not always. For many use cases, standard API calls or context injection via other formats may be more practical.
