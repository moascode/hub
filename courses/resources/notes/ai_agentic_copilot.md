# Building an Agentic Java Developer with Copilot, MCP, and OpenMemory

Lately, I’ve been experimenting with something I like to call an “agentic junior dev” — basically, wiring up GitHub Copilot with tools like MCP and OpenMemory to act more like a teammate than a typing assistant. This is especially handy for repetitive stuff in the Java world: unit testing, Sonar issue cleanup, and other boring-but-necessary tasks.

## 🧩 The Goal

I wanted Copilot to stop being just a reactive autocomplete tool. Instead, I wanted it to:

* Understand my Java project
* Write meaningful unit tests
* Fix SonarLint issues
* Keep some memory of what it's been doing

To make that happen, I’m combining a few tools that give Copilot more awareness and persistence.

## 🧠 The Stack

Here’s the setup I’m running:

### 1. **VS Code**

This is my go-to editor. Lightweight, fast, and has great Java support once you install the Java extension pack:

```sh
code --install-extension vscjava.vscode-java-pack
```

### 2. **GitHub Copilot in Agent Mode**

If you haven’t tried Agent Mode yet, do it. It turns Copilot into something more interactive. It can:

* See your project structure
* Jump between files
* Respond to instructions like "write unit tests for this class"

Just make sure you have the latest Copilot Chat extension installed and you’re signed in with Copilot Pro.

### 3. **MCP (Memory and Context Provider)**

This is where the magic happens. MCP gives Copilot some working memory:

* Remembers what files it touched
* Threads context between tasks
* Provides metadata about the codebase

You’ll need to be part of the Copilot Labs or Workspace preview to turn this on.

### 4. **OpenMemory (or your own memory layer)**

This is optional, but super useful. I’m using a simple local memory store that:

* Keeps notes like “we use Mockito for tests”
* Tracks recurring decisions
* Feeds that memory into Copilot sessions

It’s still early days, but even this lightweight memory makes a big difference.

---

## 🔧 Setup Walkthrough

Here's how I glued everything together:

### Step 1: Create a Java Project

```bash
mvn archetype:generate \
  -DgroupId=com.example \
  -DartifactId=demo \
  -DarchetypeArtifactId=maven-archetype-quickstart \
  -DinteractiveMode=false
```

### Step 2: Enable Copilot Agent Mode

* Install the Copilot Chat extension
* Use the Command Palette → `Copilot: Start Agent Chat`

### Step 3: Hook in MCP + Memory

If you’re rolling your own memory, you can set up a JSON like:

```json
{
  "project": "demo",
  "memory": [
    "Use JUnit 5 + Mockito for testing",
    "Avoid nested ternaries (Sonar)"
  ]
}
```

Feed that into your Copilot prompt early in the session. It helps guide the responses.

### Step 4: Try These Prompts

Inside your Java file:

```java
// agent: Write unit tests for this class using JUnit 5 and Mockito
```

Or:

```java
// agent: Fix all SonarLint issues in this file
```

It’s surprisingly good at reading the file, patching problems, and explaining what it’s doing.

---

## 🧪 What It's Good At

Here’s what this setup handles really well:

* ✅ Generates decent test cases with mocks/stubs
* ✅ Fixes most Sonar issues automatically
* ✅ Writes method-level JavaDoc
* ✅ Refactors long methods or cleans up bad naming

---

## 🚀 Final Thoughts

This setup isn’t magic, but it feels close. It won’t replace a human junior dev — yet — but it does help me offload the mechanical stuff so I can focus on actual engineering.

If you work in Java and constantly find yourself writing boilerplate tests or cleaning up Sonar warnings, this is worth trying. Copilot with memory feels less like autocomplete, and more like pair programming with someone who actually remembers what you told them five minutes ago.

Let me know if you try a similar setup or if you’ve figured out better ways to plug memory into the flow.
