<div align="center">

# Scrapzz

**From university websites to structured study-programme data.<br/>Headless scraping · Gemini extraction · validation in Python**

Built at **iMEDiA Group** · React frontend + FastAPI backend

<br/>

![React](https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white)
![Playwright](https://img.shields.io/badge/Playwright-2EAD33?style=for-the-badge&logo=playwright&logoColor=white)
![Crawl4AI](https://img.shields.io/badge/Crawl4AI-263238?style=for-the-badge)
![Gemini API](https://img.shields.io/badge/Gemini_API-8E75B2?style=for-the-badge)
![Pydantic](https://img.shields.io/badge/Pydantic-E92063?style=for-the-badge&logo=pydantic&logoColor=white)

![Project](https://img.shields.io/badge/project-portfolio_case_study-64748B?style=flat-square)
![Scope](https://img.shields.io/badge/scope-frontend_%2B_backend-1f6feb?style=flat-square)
![Testing](https://img.shields.io/badge/testing-Pytest_%2B_GitHub_Actions-2ea44f?style=flat-square)

<br/>

[About](#about) &nbsp;·&nbsp; [Features](#features) &nbsp;·&nbsp; [Workflow](#workflow) &nbsp;·&nbsp; [My contribution](#contribution) &nbsp;·&nbsp; [Testing](#testing)

</div>

---

<a id="about"></a>

## 📌 About

**Scrapzz** is an internal study-programme data aggregator built at **iMEDiA Group**. It collects information from Polish university websites and presents it as structured records in a React interface.

University pages differ in layout, often render content with JavaScript, and spread programme details across multiple sections. Scrapzz combines browser-based collection, LLM extraction and deterministic processing to bring that information together.

> [!NOTE]
> This repository is a **portfolio case study** covering the application, engineering decisions and my contribution. It does not contain the implementation code.

<a id="features"></a>

## ✨ Features

| | Feature | What it does |
|:--:|---|---|
| 🔎 | **Programme discovery** | Finds programme pages in a university catalogue, filters unrelated links and falls back to HTML when link extraction returns no results. |
| 🌐 | **Headless collection** | Uses Crawl4AI and Playwright to load source pages, including JavaScript-rendered content. |
| 🧠 | **Structured extraction** | Gemini extracts programme fields; Pydantic validates the schema and Python normalizes selected values. |
| 💰 | **Tuition handling** | Normalizes fee information and supplements extraction with source-specific HTML fallbacks. |
| 🗂️ | **Review interface** | Displays scan statistics and expandable cards with descriptions, fees, specializations and source links. |
| 🧩 | **Partial results** | Keeps successful programme records when another page fails, returning per-page errors alongside the results. |

<a id="workflow"></a>

## 🧭 How it works

<p align="center">
<b>🔗 Catalogue URL</b> &nbsp;→&nbsp; <b>🔎 Discover</b> &nbsp;→&nbsp; <b>🌐 Collect</b><br/>
↓<br/>
<b>🧠 Extract</b> &nbsp;→&nbsp; <b>🧪 Validate</b> &nbsp;→&nbsp; <b>🗂️ Review</b>
</p>

<details>
<summary><b>Follow a scan from URL to programme cards</b></summary>

<br/>

1. **Start a scan.** The user enters a university programme-catalogue URL in the React interface.
2. **Discover programme pages.** Crawl4AI and Playwright load the catalogue. Gemini helps identify programme links; deterministic filters remove unrelated links, with an HTML fallback when link extraction returns no results.
3. **Collect source content.** The crawler visits programme pages in a headless browser and prepares their content for extraction.
4. **Extract and validate.** Gemini returns structured programme data, Pydantic validates the schema, and Python normalizes selected fields such as tuition fees and study modes. Source-specific HTML fallbacks supplement tuition extraction.
5. **Review results.** The interface shows scan statistics and expandable programme cards, including descriptions, tuition information, specializations and source links.

**Extracted fields:** programme name, degree level, study mode, number of semesters, faculty, language, specializations, admission requirements and tuition fees.

</details>

<details>
<summary><b>⚙️ Engineering decisions</b></summary>

<br/>

### Rendering before extraction

Playwright, used through Crawl4AI, supports pages whose programme listings or tuition information depend on JavaScript. The LLM receives processed page content rather than replacing the browser-based collection step.

### Model output followed by code

The pipeline separates LLM extraction from schema validation and deterministic normalization. Link filters and tuition-related fallbacks handle specific cases in code rather than relying only on prompt instructions.

### Partial results instead of an all-or-nothing scan

A failure on one programme page does not discard successful results from other pages. The backend returns successful records alongside per-page errors, while the interface exposes scan statistics.

### A frontend for inspecting the output

The React interface presents found, processed and successful programme counts. Expandable records expose the extracted details and source URLs so the results can be reviewed.

</details>

<a id="contribution"></a>

## 👨‍💻 My contribution

I built the **end-to-end system**: the scraping pipeline, FastAPI backend, Gemini extraction with Pydantic validation, and a React interface for starting scans and reviewing results.

**Stack:** React, Vite, Python, FastAPI, Playwright, Crawl4AI, Gemini API, Pydantic, Pytest and GitHub Actions.

<a id="testing"></a>

## 🧪 Testing

- **Regression coverage:** deterministic Pytest tests for link filtering, normalization, tuition extraction, catalogue discovery and export mapping.
- **Fixture-based checks:** tests run without live crawling or Gemini calls.
- **Continuous integration:** GitHub Actions runs the suite on pushes to `main` and on pull requests.

<details>
<summary><b>📋 Known limitations</b></summary>

<br/>

- University layouts vary, so new sources may require adjustments to extraction heuristics.
- Some dynamically loaded tuition information needs source-specific handling.
- Schema validation checks structure and types; it does not independently establish that every extracted fact is correct. LLM output still needs review against the source.

</details>

---

## 🤝 Contact

**Antoni Krawczyk** — Frontend & AI Developer

[LinkedIn](https://www.linkedin.com/in/antoni-krawczyk-62224539a) · [GitHub](https://github.com/AntoniKra)
