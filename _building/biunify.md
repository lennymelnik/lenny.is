---
layout: building
title: BIUnify
description: Transform Excel, CSV, and JSON into live REST API data.
date: 2024-12-01
image: /assets/biunify/screenshot.png
---

BIUnify is an application built on **Bun**, **Postgres**, **Hono**, and **HTMX** that lets you upload Excel, CSV, or JSON files and immediately access the data through a standard REST API. In many business environments, spreadsheets are constantly changing, which makes it difficult to keep downstream applications, integrations, or reports up to date. I ran into this problem all the time in my everyday work, so I built BIUnify to solve it.

> **Use cases:**  
> - Real-time integrations with BI tools  
> - Automating report generation  
> - Powering dashboards without manual exports  

Although it’s still in beta, BIUnify already works great, and I’ve started getting interest from a few companies.

---

## Why Bun & HTMX?

I chose **Bun** and **HTMX** because I wanted to explore lightweight, high-performance frameworks while keeping the web app minimal yet fully functional. During development, I learned a ton about:

1. Designing efficient, RESTful APIs  
2. Handling file uploads and parsing spreadsheets  
3. Leveraging Hono for routing and middleware  
4. Using HTMX to update the UI without a heavy frontend bundle  

Overall, building BIUnify was an amazing experience and I’m excited to keep refining it.