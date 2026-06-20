# 🎯 Customer Feedback Automation Workflow

> **Automatically collect, classify, and store customer feedback — and reward your happiest customers with discounts.**

---

## 📋 Overview

This **n8n** workflow powers a seamless feedback pipeline for **Product X**. Customers fill out a simple form, their response is instantly classified, and everything gets neatly logged to Google Sheets — with positive reviewers automatically flagged for a discount.

---

## 🗺️ Workflow Architecture

```
📝 Form Submission
        │
        ▼
   🔀 IF Node
  (Feedback == "Positive"?)
        │
   ┌────┴────┐
   ▼         ▼
✅ YES      ❌ NO
Give_Discount=Yes   Give_Discount=No
        │         │
        └────┬────┘
             ▼
     📊 Google Sheets
      (Append Row)
```

### 📸 Workflow Preview

![n8n Workflow Screenshot](./workflow_screenshot.jpg)

---

## ⚙️ Nodes Breakdown

| Node | Type | Description |
|------|------|-------------|
| 📝 **On form submission** | Form Trigger | Captures customer input via a web form |
| 🔀 **If** | Conditional | Checks if feedback is `"Positive"` |
| ✅ **Discount_YES** | Set | Tags the record with `Give_Discount = Yes` |
| ❌ **Discount_No** | Set | Tags the record with `Give_Discount = No` |
| 📊 **Append row in sheet** | Google Sheets | Saves all data to a Google Spreadsheet |

---

## 📝 Form Fields

The feedback form (`Test Form For feedBack`) collects the following fields:

| Field | Type | Required |
|-------|------|----------|
| `Email_Id` | Email | ✅ |
| `Name` | Text | ✅ |
| `Age` | Number | ✅ |
| `FeedBack` | Dropdown | ✅ |

### FeedBack Options
- 😊 **Positive**
- 😐 **Neutral**
- 😞 **Negative**

---

## 📊 Google Sheets Schema

Data is appended to **Sheet1** with the following columns:

| Column | Source |
|--------|--------|
| `Email_Id` | Form input |
| `Name` | Form input |
| `Age` | Form input |
| `FeedBack` | Form input |
| `Give_Discount` | Computed (`Yes` / `No`) |

---

## 🚀 How to Use

### 1. Import the Workflow
```bash
# In n8n, go to:
# Workflows → Import → Upload `My_workflow.json`
```

### 2. Connect Your Google Account
- Open the **"Append row in sheet"** node
- Under **Credentials**, connect your **Google Sheets OAuth2** account

### 3. Set Your Spreadsheet
- Point the node to your target Google Spreadsheet
- Make sure **Sheet1** has the correct column headers (see schema above)

### 4. Activate & Share the Form
- Click **Publish** to activate the workflow
- Share the form URL with your customers and start collecting responses!

---

## 🔧 Customization Tips

- **Add more feedback options** — Edit the `FeedBack` dropdown in the Form Trigger node
- **Expand discount logic** — Add branches in the `If` node for Neutral feedback too
- **Send email notifications** — Attach a Gmail/SMTP node after `Discount_YES` to auto-send discount codes
- **Add a Slack alert** — Notify your team in real-time when negative feedback arrives

---

## 📦 Tech Stack

- **[n8n](https://n8n.io)** — Workflow automation platform
- **Google Sheets** — Data storage & reporting
- **n8n Form Trigger** — No-code customer-facing form

---

## 📄 License

This workflow is for internal use. Feel free to adapt it for your own projects!

---

<div align="center">

Made with ❤️ using **n8n**

</div>
