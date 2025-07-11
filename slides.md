---
theme: geist
---

<style>
.slidev-page {
  margin-left: 40px !important;
}

.slidev-code {
  max-height: auto !important;
  overflow: auto !important;
  font-size: 0.8rem !important;
  max-width: calc(100% - 80px) !important;
  margin: 0 !important;
}

pre {
  max-height: 300px !important;
  overflow: auto !important;
  font-size: 0.8rem !important;
  max-width: calc(100% - 80px) !important;
  margin: 0 !important;
}

code {
  font-size: 0.8rem !important;
}

h1, h2, h3 {
  margin-bottom: 0.5rem !important;
}

h1 + ul, h2 + ul, h3 + ul, h1 + p, h2 + p, h3 + p {
  margin-top: 0.25rem !important;
}
</style>

# Use Cursor like a 🥷

Master your code editor skills

Corentin Le Berre

---

# What we'll cover

This presentation will be covering the following areas

- 🎯 **Cursor Rules** - fine tune your IDE LLM
- 🔌 **Do you need MCP?** - use cases for developers and non-developers, security warnings
- 🛠 **Building MCPs** - How to create your own MCP

---

# 🎯 **Cursor Rules**

Cursor Rules let you customize how the AI assistant behaves in your projects

**Setup**: <KBD>⌘</KBD> + <KBD>shift</KBD> + <KBD>j</KBD> → Rules & Memories

### Project-Level Rules

- Create `.cursor/rules` file in your project root
- Define coding standards, patterns, and preferences for your team. Cursor will follows these rules automatically

### Users rules

- Apply across all projects for personal coding style preferences

<div v-click>

**Simple examples** :

- *"Use TypeScript, functional components, Tailwind CSS, and never use classes when generating styles"*
- *"Never put comments in the code unless explicitly asked to."*


</div>
---

# 🎯 **Cursor Rules**

Cursor Rules let you customize how the AI assistant behaves in your projects

```md
---
alwaysApply: true
---

Write concise, technical TypeScript. Follow Standard.js rules.

Use functional, declarative patterns; avoid classes.

Favor loops and small helper modules over duplicate code.

Use descriptive names with auxiliary verbs (e.g. isLoading, hasError).

File layout: exported component → subcomponents → hooks/helpers → static content.
```

**templates** :
examples on <https://dotcursorrules.com> or generate your own with **/Generate Cursor Rules**

---

# 🔌 **Do you need MCP?**

## What is MCP?

<div v-click>

**Model Context Protocol** (open standard introduced by Anthropic) - Think of it as **USB-C for AI**

- **Universal connector** that lets AI tools talk to each other
- **Standardized way** to share data, functions, and resources between applications
- **One protocol** to connect databases, APIs, file systems, and more to any AI assistant

</div>

<div v-click>

## Do you need it?

Short answer : **No** (for most people)

</div>

---

# Thanks for listening! 🙏

**Questions & Discussion**

---

# 🔌 **Do you need MCP?**

## My developer use cases

- 🐘 **PostgreSQL** - Give AI automatic feedback when writing complex SQL Queries (read only)
- 🌐 **Browser Control** - Debug your components with full access to your browser DOM, console etc
- 🐳 **Docker** - Dont read horrible errors again
- 🎭 **Playwright** - Automate web testing and interactions quickly
- 📚 **Context7** - Give your LLM ✨fancy up-to-date✨ documentation

<div v-click>

**And why not?**

- 🎵 **Spotify** - Create the best playlist for the chalet
- 🏠 **Airbnb** - Plan your next holidays
- 🗺️ **Google Maps** - Find the best coffee in town for your next date

</div>

<div v-click>

<div><Button>Quick demo</Button></div>

</div>

---

# 🛠 **Building MCPs**

Building an MCP is surprisingly simple! Here's a complete example:

```ts {1-9|10-26|all}
#!/usr/bin/env node
import { McpServer } from "@modelcontextprotocol/sdk/server/mcp.js";
import { StdioServerTransport } from "@modelcontextprotocol/sdk/server/stdio.js";

const server = new McpServer({
  name: "mcp-demo",
  version: "1.0.0",
});

server.registerTool(
  "sum",
  {
    title: "Sum Calculator",
    description: "Calculate the sum of two numbers",
    inputSchema: {
      a: { type: "number", description: "First number" },
      b: { type: "number", description: "Second number" },
    },
  },
  async ({ a, b }) => {
    const result = a + b;
    return {
      content: [{ type: "text", text: `${a} + ${b} = ${result}` }],
    };
  }
);

await server.connect(new StdioServerTransport());
```

---

# 🛠 **Building MCPs**

**Setup**: <KBD>⌘</KBD> + <KBD>shift</KBD> + <KBD>j</KBD> → Tools & Integrations → Model Context Protocol → New MCP Server

```json
{
  "mcp-demo": {
    "command": "npx",
    "args": ["."],
    "cwd": "/path/to/your/mcp/project"
  }
}
```

<div v-click>

**⚠️ MCPs run with your user privileges - Only use trusted sources!**

</div>

<div v-click>

**💡Pro Tip: Don't forget to add a rule!**

```md
When you need to sum two numbers use the mcp mcp-demo
```

</div>

<div v-click>

<div><Button>Quick demo</Button></div>

</div>

---

# 📚 **Resources**

## Cursor Rules & Documentation

- 🌐 **Cursor Rules Templates** - <https://dotcursorrules.com>
- 📖 **Cursor Documentation** - <https://docs.cursor.com>

## MCP (Model Context Protocol)

- 🔌 **MCP documentation** - <https://modelcontextprotocol.io>
- 📦 **MCP typescript SDK on GitHub** - <https://github.com/modelcontextprotocol/typescript-sdk>

---

# Thanks for listening! 🙏

**Questions & Discussion**
