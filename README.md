
# Optimizing Documentation for RAG-Based Chatbot Retrieval

Improving chatbots often comes down to improving their ability to retrieve the best answer to a user's question. One way to do this is by using Retrieval-Augmented Generation (RAG). But RAG starts before you write any code - it starts with the content itself. Here, I take an existing document and optimize it for a chatbot by restructuring it so the information is easier to retrieve and use. This helps the chatbot surface better answers, leading to a better user experience when a user's question is answered.

Here is a concrete example of that approach. In this README, I take an excerpt from an existing technical document and refactor it into independent, retrievable units for AI-powered search and chat.

Using Xfinity's public support documentation, I illustrate how fragmented information prevents effective retrieval and how you can restructure content into standalone, retrievable units.

> **Note:** Although I used the Xfinity chatbot as an example of retrieval failure, this demonstration assumes the chatbot retrieves answers from public-facing help documentation. In reality, the chatbot may use a combination of public docs, internal knowledge bases, and training data. Regardless of the specific implementation, this project demonstrates why fragmented content leads to poor retrieval results and how to optimize any documentation—whether public or internal—for RAG-based systems.

## Section 1: The Problem

**User Query:** "Why does my internet stop working after I changed my WiFi password?"

**Xfinity Chatbot Response:** [Generic troubleshooting response that doesn't answer the question]

### Why the chatbot doesn't answer the question correctly

When a user asks "Why does my internet stop working after I changed my WiFi password?", the chatbot searches its database (such as help docs) for answers that match the context of the user's question.

**The problem:** The complete answer doesn't exist in one place. The information is scattered across multiple articles:

- One article mentions checking if your password changed (but doesn't explain why this causes issues)
- Another article explains how to change your password (but doesn't mention what happens to connected devices)
- A third article discusses connecting to the correct network (but not in the context of password changes)

Because the chatbot cannot find a single chunk of content that directly addresses "password change causing connectivity issues," it retrieves a more generic answer—like general troubleshooting steps or instructions for changing passwords—neither of which answers the user's actual question.

**The solution** is to create standalone answer units where all the information needed to answer a specific question exists in one retrievable chunk.

But first, what is the answer to the user's question, which the chatbot should have answered?

### Let's find the answer by reading the docs

**Here is one part:**

From the "Xfinity Internet and WiFi connection troubleshooting" article, included in a long list of tips:

> "Check if the WiFi network name and password were changed, and update your personal device WiFi settings to the new name and password, if necessary."

**Here is another part:**

From the "Changing advanced WiFi settings in the Xfinity app" article, under "Change WiFi name" section:

> "Select Edit WiFi settings from the pop-up card to edit your WiFi name and password, change security settings and choose whether you hide or broadcast your WiFi name. Once finished, select Save."

**And here is a third part:**

From the "Managing and optimizing your WiFi network" article, under "Confirm your device is connected to your in-home WiFi network":

> "Go to the WiFi settings of your personal device to make sure you're connected to your personal WiFi network."

### So, what is the answer to the user's question?

When you change your WiFi password, all devices that were previously connected to your network are still trying to use the old password. They can't connect with the old credentials, so they appear to have no internet connection. You need to manually update the WiFi password on each device to reconnect them to your network.

## How could we optimize the docs to help a RAG-based chatbot get the answer correct?

### Common RAG Optimization Approaches

1. **Decomposition (Breaking down large docs)**
   - Take existing long documents
   - Break them into smaller, topic-focused chunks
   - Each chunk addresses one specific question/topic

2. **Recomposition (Combining scattered info)**
   - Take information scattered across multiple docs
   - Combine related pieces into complete, standalone units
   - Fill gaps where information is missing

3. **Metadata enrichment**
   - Add structured metadata to chunks (keywords, topics, question types)
   - Helps retrieval systems find relevant content

4. **Q&A pair creation**
   - Convert documentation into explicit question-answer pairs
   - Each pair is a retrievable unit

5. **Hierarchical structuring**
   - Organize content in parent-child relationships
   - Use summaries at top level, details nested below

RAG improves chatbots and search by using context in the form of vectors. However, to create effective vectors, the source text first needs to be organized into the correct chunks or units that can answer the questions at hand.

When breaking down content like this, you need to break it down into units which stand alone.

Although we could just add the exact question and answer to the docs, that is not a great approach in the long run. If you did that for every question a user might ask, the documentation would become unmanageable.

A better way here would be to look at it from a context standpoint and recombine the existing content into different chunks.

### Here's how to restructure the existing fragments

**Instead of three separate fragments in three different articles:**

- Fragment about checking if password changed (in troubleshooting)
- Fragment about how to change password (in settings)
- Fragment about connecting to network (in optimization)

**Step 2. Create a contextual unit about "WiFi Password Changes and Device Connectivity":**

#### Recombined Contextual Unit: "WiFi Password Changes and Device Connectivity"

When you change your WiFi network password through the Xfinity app (Select Edit WiFi settings from the pop-up card to edit your WiFi name and password, change security settings and choose whether you hide or broadcast your WiFi name), all devices previously connected to your network will need to be updated.

If your internet appears to stop working after changing your WiFi password, this is because your devices are still attempting to connect using the old password. Check if the WiFi network name and password were changed, and update your personal device WiFi settings to the new name and password.

**To reconnect your devices:**

1. Go to the WiFi settings of your personal device
2. Make sure you're connected to your personal WiFi network (not a public Xfinity WiFi hotspot like xfinitywifi or XFINITY)
3. Enter the new password
4. Repeat for each device that needs internet access

---

Here, we needed to add some new content because the existing documentation did not include all the details required to answer the question in a way that could stand on its own. Adding content is a valid part of optimizing documentation for RAG-based retrieval, particularly when recomposing fragmented information into complete, standalone units.

### Why Adding Content is Valid for RAG Optimization

- **Fills knowledge gaps** - If users are asking questions the docs don't answer, the content needs to be added
- **Provides necessary context** - RAG systems need complete context in each chunk. If the "why" or "how" is missing, you need to add it
- **Makes implicit knowledge explicit** - Subject matter experts often leave out "obvious" connections that users (and RAG systems) need spelled out
- **Creates standalone units** - Sometimes you can't make something standalone without adding connecting information
- **Real-world necessity** - In practice, documentation gaps are common. Optimization often means both restructuring AND filling gaps

Though we only answered one user's question in this educational demo, we could use the same approach to optimize help docs or other types of documents to make the chatbot answers more useful to anyone who uses them.

## About this example

This README contains one brief illustrative example to demonstrate how documentation can be refactored to improve retrieval for RAG-based chatbots.

In a real production environment, this work would typically be done within an existing documentation system such as Confluence or a similar internal knowledge base. In those systems, hierarchy is signaled through structured headings (H1, H2, H3), which allows large documents to be broken into smaller, retrievable sections or subsections.

For example, within a Python formatting style guide, a subsection such as "Formatting Lists in Python" could be written as a smaller, self-contained section under a broader "Python Formatting" heading. This allows a chatbot to retrieve only the relevant subsection when a user asks a specific question like, "How do I format a list in Python at this company?", rather than returning the entire style guide.

In addition to hierarchy, metadata can further improve retrieval. In Confluence, this is often done using labels or tags attached to a page.

### Front-matter / metadata section (common workaround)

In systems like Google Docs, which do not support native labels, similar signals can be provided through clear document naming conventions. In some cases, each standalone chunk can also be modeled as a separate document, allowing the document title itself to function as lightweight metadata.

As an alternative or complement, suggested metadata (such as system name, topic, or content type) can also be included at the top of a document as plain text. This makes the intent clear to human readers and allows metadata to be evaluated or formalized downstream during ingestion into other systems.

**Example:**
```
Document type: Troubleshooting
System: Employee Portal
Audience: Internal employees
Last reviewed: 2026-01-15
Owner: IT Support
```

*In practice, teams often add a small metadata block at the top of the doc.*

This is human-readable metadata that:

- can be scraped later
- can be converted into labels if the doc moves to Confluence
- can help reviewers immediately

### If you take this approach, remember to use consistent naming conventions

**Examples:**

- `Employee-Portal_Access_Troubleshooting`
- `Python-Formatting_Style-Guide`
- `VPN_Access_Internal`

*Since Docs lacks labels, file naming becomes metadata.*

This helps:

- search
- organization
- later ingestion into RAG pipelines
