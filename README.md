# 🏢 ERP mock_demo

> A lightweight, browser-based mock of an Enterprise Resource Planning frontend — built as the **automation target** for an RPA + AI integration thesis project.

---

## 📌 Overview

`erp-mock-demo` is a single-page HTML/CSS/JS application that simulates the procurement module of an Enterprise Resource Planning system. It was designed specifically to serve as a **realistic, controllable web target** for a UiPath RPA bot, which authenticates, fills out forms, and extracts generated Purchase Order numbers — all as part of a broader BPM + RPA + AI automation pipeline.

The application deliberately keeps its stack minimal (zero dependencies, zero build tools) to ensure maximum portability and predictability during automated interaction.

---

## 🎯 Purpose & Context

This project is the **frontend mock layer** of a thesis automation system titled:

> *"Integrazione tra Business Process Management (BPM), Robotic Process Automation (RPA) e Intelligenza Artificiale (AI)"*

The full automation pipeline works as follows:

```
Jamio (BPM) ──► triggers UiPath bot ──► interacts with this ERP mock ──► extracts PO Number ──► returns result to BPM process
```

The mock app provides a stable, reproducible ERP interface so the RPA bot can be developed and tested without depending on a real enterprise system.

---

## ✨ Features

| Feature | Description |
|---|---|
| 🔐 Authentication | Login screen with hardcoded demo credentials |
| 📋 Purchase Order Form | Multi-field form with validation logic |
| 🏷️ PO Number Generation | Auto-generated unique PO codes (e.g. `PO-2025-84732`) |
| ✅ Validation Rules | Material Code must follow `MAT-XXXXX` format |
| 💾 LocalStorage Persistence | Created orders are saved in the browser |
| 🤖 Bot-Friendly Design | Success message stays visible until manually dismissed — designed for RPA scraping |

---

## 🖥️ Application Structure

```
erp-mock-demo/
│
├── index.html          # Single-file application (HTML + CSS + JS)
│
└── README.md           # This file
```

The entire application lives in a **single self-contained HTML file** with no external dependencies, frameworks, or build steps.

---

## 🚀 Getting Started

### Prerequisites

- Any modern web browser (Chrome, Firefox, Safari, Edge)
- No installation, no package manager, no server required

### Run locally

```bash
# Clone the repository
git clone https://github.com/raffytorres96/erp-mock-demo.git

# Open the file directly in your browser
open index.html
```

Or simply **double-click** `index.html` on your filesystem.

---

## 🔐 Demo Credentials

The login page accepts the following hardcoded credentials:

| Field | Value |
|---|---|
| Username | `bot_user` |
| Password | `bot_password` |

> ⚠️ These credentials are intentional and publicly visible — this is a mock application with no real backend or sensitive data.

---

## 📝 Creating a Purchase Order

Once logged in, fill in the following fields:

| Field | Type | Validation |
|---|---|---|
| **Material Code** | Text | Must start with `MAT-` (e.g. `MAT-12345`) |
| **Description** | Text | Free text (e.g. `Laptop HP EliteBook 840`) |
| **Quantity** | Number | Minimum value: `1` |
| **Vendor** | Dropdown | One of 4 predefined vendors |
| **Cost Center** | Dropdown | One of 4 predefined department codes |

On successful submission, the application displays the generated PO Number and keeps it visible — intentionally designed so that an RPA bot can scrape it without time constraints.

---

## 🤖 RPA Integration Notes

This mock was built with the following RPA-specific design decisions:

- **Stable DOM selectors** — all interactive elements have explicit `id` attributes for reliable UiPath targeting
- **No timeouts on success screen** — the PO confirmation stays displayed until the user manually dismisses it, giving the bot ample time to read the value
- **Predictable flow** — login → form → confirmation, no dynamic redirects or popups
- **LocalStorage as mock DB** — each PO is stored with its full JSON payload, accessible via browser DevTools if needed for debugging

### UiPath selector examples

```xml
<!-- Login button -->
<webctrl tag='BUTTON' type='submit' />

<!-- PO Number output -->
<webctrl id='poNumber' tag='DIV' />

<!-- Material Code input -->
<webctrl id='materialCode' tag='INPUT' />
```

---

## 🗂️ Data Model

Each created Purchase Order is stored in `localStorage` with the following structure:

```json
{
  "poNumber": "PO-2025-84732",
  "materialCode": "MAT-12345",
  "description": "Laptop HP EliteBook 840",
  "quantity": "10",
  "vendor": "Tech Supply Corp",
  "costCenter": "CC-IT-2025",
  "createdAt": "2025-04-01T10:23:45.000Z",
  "status": "Created"
}
```

---

## 🔧 Available Vendors

```
Tech Supply Corp
Office Solutions Ltd
Global Procurement Inc
Industrial Parts Co
```

## 🏛️ Available Cost Centers

```
CC-IT-2025   →  IT Department
CC-HR-2025   →  Human Resources
CC-OPS-2025  →  Operations
CC-MKT-2025  →  Marketing
```

---

## 🧪 Manual Test Scenario

To verify the application works correctly:

1. Open `index.html` in a browser
2. Log in with `bot_user` / `bot_password`
3. Fill the form:
   - Material Code: `MAT-00001`
   - Description: `Test Item`
   - Quantity: `1`
   - Vendor: `Tech Supply Corp`
   - Cost Center: `CC-IT-2025`
4. Click **Save Purchase Order**
5. Confirm a `PO-YYYY-XXXXX` number appears on screen
6. Open browser DevTools → Application → LocalStorage to inspect the saved record

---

## 📚 Related Projects & Thesis Context

This mock is one component of a larger academic project. The full system integrates:

| Component | Technology | Role |
|---|---|---|
| BPM Platform | Jamio | Process orchestration & workflow definition |
| RPA Bot | UiPath Studio + Orchestrator | Automated interaction with this ERP mock |
| AI Layer | LLM integration | Intelligent decision-making within the workflow |
| ERP Mock | This repository | Automation target frontend |

---

## 👤 Author

**Raffaele Torres**
Computer Science Graduate — University of Bari
Thesis: *BPM + RPA + AI Integration*

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=flat-square&logo=linkedin&logoColor=white)](www.linkedin.com/in/raffaele-gatta-a27bb0178)
[![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/raffytorres96)

---

## 📄 License

This project is released for **academic and demonstration purposes only**.

---

<p align="center">
  <img src="https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5&logoColor=white"/>
  <img src="https://img.shields.io/badge/CSS3-1572B6?style=flat-square&logo=css3&logoColor=white"/>
  <img src="https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black"/>
  <img src="https://img.shields.io/badge/UiPath-FA4616?style=flat-square&logo=uipath&logoColor=white"/>
  <img src="https://img.shields.io/badge/BPM-Jamio-6B46C1?style=flat-square"/>
</p>
