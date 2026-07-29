# 🚀 [Tips Hindawi](https://www.tipshindawi.com/) Challenge (June–July) 2026

> 🏆 This repository is my official submission for the [ **Tips Hindawi** ](https://www.tipshindawi.com/) **Challenge (June–July) 2026**.

## 👤 Participant

| Field            | Value                                |
| ---------------- | ------------------------------------ |
| Full Name        | Anas Tarek Helmi Rezk                                      |
| Project Name     | InvoScan                                    |
| GitHub Username  | AnasTarek25                                    |
| Challenge Batch  | June–July 2026                       |
| Training Program | Large Language Models (LLMs) Program |
| Organization     | [**Edrak for Ai**](https://edrak4ai.com/en)                         |

---

# 📖 Project Overview

Briefly describe your project.

---

# ✨ Features
* **Automatic text extraction** from PDF or image invoices — native text extraction for digital PDFs via `pdfplumber`, with a Tesseract OCR fallback for scanned documents/images (Arabic text is stripped out of the bilingual invoice so only the English content is parsed)
  
* **Deterministic, template-specific parsing** of the Al-Tazaj invoice layout (invoice number, invoice date, and every line item) using regex — instant, with no LLM/GPU call needed for the normal case
  
* **Automatic confidence checking** on every parsed row: quantity × unit price is cross-checked against the invoice's stated amount, and any row that's off is flagged `low_confidence` (usually a sign of an OCR misread digit) so it can be manually reviewed
  
* **Rule-based product categorization** across built-in categories (Chicken, Beverages, Desserts, Burgers & Sandwiches, Salads & Vegetables, Sauces & Condiments, Coating & Ingredients), with an **LLM fallback** for any item that doesn't match a known keyword
  
* **Full LLM extraction fallback** — if the regex parser can't find a single line item at all (e.g. the document isn't the expected template), the LLM extracts the entire invoice instead
  
* **SQLite-backed database viewer** to browse a single stored invoice's line items, or every invoice at once
  
* **Cross-invoice aggregation** that sums matching line items (e.g. the same product ordered on more than one invoice) into one combined total per product
  
* **Expandable per-item breakdown rows** in the aggregated view — any item summed across more than one invoice is tagged, and expanding it shows exactly which invoice(s) it came from and what each contributed
  
* **One-click public deployment** straight from Google Colab via an ngrok tunnel, no separate hosting required


---

# 🛠️ Technologies Used

* **Python** — core language
* **Streamlit** — web application UI
* **Transformers, PyTorch, bitsandbytes** — running the 4-bit quantized `Mistral-7B-Instruct-v0.2` model for LLM-assisted extraction/categorization
* **pdfplumber, pytesseract, pdf2image, Pillow** — PDF parsing and OCR text extraction
* **SQLite3** — local invoice/line-item storage
* **pandas** — data aggregation and tabular display
* **json-repair** — repairing slightly malformed JSON returned by the LLM
* **ngrok** — public tunneling of the Streamlit app from Google Colab
* **Kaggle (GPU runtime)** — execution environment


---

# ⚙️ Installation

1. Open the notebook in **Kaggle** and switch the runtime to a **GPU** instance (required for the LLM fallback).
2. Run the setup cells in order — these install the Linux system packages (`poppler-utils`, `tesseract-ocr`) and the required Python libraries (`transformers`, `torch`, `accelerate`, `bitsandbytes`, `pdfplumber`, `pytesseract`, `pdf2image`, `pillow`, `streamlit`, `pyngrok`, `json-repair`, `pandas`, `sentencepiece`).
3. Run the **LOAD LLM** cell to download and cache the 4-bit Mistral model to disk.
4. Run the cell that writes out `app.py` (the Streamlit application code).
5. Get a free auth token from [ngrok.com](https://ngrok.com), then run the final **tunneling & execution** cell — either set it as the `NGROK_AUTH_TOKEN` environment variable beforehand, or enter it when prompted.


---

# 🚀 Usage

1. Run the notebook's final cell — it starts the Streamlit server and prints a public ngrok URL.
2. Open that URL in your browser.
3. **Upload & Ingest tab:** upload a PDF, PNG, or JPG invoice, click **Process Invoice**, and review the parsed result (any low-confidence rows are called out), then save it to the database.
4. **Database Viewer & Aggregator tab:** choose a specific invoice from the dropdown to see its own line items, or choose **All Invoices** to see every stored invoice's items aggregated by category — expand any item to see which invoice(s) it was combined from.


---

# 📸 Demo

<img width="1841" height="718" alt="image" src="https://github.com/user-attachments/assets/bd42cc17-8455-44ca-a2be-625cd3496b9a" />
<img width="1883" height="884" alt="image" src="https://github.com/user-attachments/assets/d753d4ba-b697-4650-836a-674c97c08ce5" />
<img width="1864" height="874" alt="image" src="https://github.com/user-attachments/assets/0d50ed1e-aaff-45d9-acbb-d258dc14861f" />



---

# 📈 Results

By parsing with regex first and only calling the LLM when the deterministic path can't handle a row or an entire invoice, InvoScan keeps the common case fast and fully deterministic (no hallucination risk on well-formed invoices), while still being able to fall back gracefully on categorization edge cases or unfamiliar layouts. The confidence-checking step (qty × unit price vs. stated amount) surfaces likely OCR errors instead of silently trusting bad data, and the cross-invoice aggregation with per-invoice traceability makes it possible to see combined totals for a product while still being able to audit exactly which invoices contributed to that total.

---

# 🔮 Future Improvements

* To connect it to a full irl database so it works 100% on its own 
* An Ability to check or correct the items before its inserted into the database
* apllying it into an ai automated workflow so all the user should do is to send the invoice pdfs and wait for it to be added to the database
* Add an AI inventory system where at the end of each day  the user types in the stock that has been used to the LLM and it auto sorts everything and tells u what u should buy at the end of the week / month

---

# 📚 About the Challenge

This project was developed as part of the [**Tips Hindawi**](https://www.tipshindawi.com/) **Challenge (June–July) 2026**.

[Tips Hindawi](https://www.tipshindawi.com/) is the internships department of [**Edrak for Ai**](https://edrak4ai.com/en), and the challenge encourages participants to build real-world projects, apply practical skills, and showcase their work through GitHub.

For more information about the challenge, training programs, and upcoming batches, visit the official [Tips Hindawi](https://www.tipshindawi.com/) website.

---

# 📄 License

This project is shared for educational and portfolio purposes.
