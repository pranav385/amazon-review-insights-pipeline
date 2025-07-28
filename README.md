# 📦 Amazon Review Insights Pipeline

An end-to-end pipeline to extract, clean, and analyze Amazon product reviews using Python, Selenium, pandas, and a local LLM (Ollama with LLaMA3). The pipeline extracts insights such as **sentiment**, **aspects mentioned**, **pain points** from raw customer reviews.

---

## 🔧 Tech Stack

- **Language**: Python  
- **Tools**: Jupyter Notebook, Selenium, BeautifulSoup, pandas, regex  
- **LLM**: Ollama (LLaMA3 model)  
- **Output Analysis**: Power Query (Excel)

---

## 🗂️ Project Structure

This project consists of **6 Jupyter notebooks**, each responsible for one step in the pipeline:

### 1️⃣ `1_Extract_Amazon_Data.ipynb`
- Crawls Amazon search results and product review pages
- Extracts product metadata and reviews
- Saves output to: `product_laptop.csv`

### 2️⃣ `2_Clean_Amazon_Data.ipynb`
- Cleans and preprocesses raw review data
- Removes duplicates, formats text, and adds metadata
- Saves output to: `Cleaned_laptop_df.csv`

Note: For efficient local LLM processing (LLaMA 3 via Ollama), I intentionally sampled a limited number of reviews per product. This trade-off ensured faster, high-quality insight generation while maintaining system performance. The pipeline remains scalable for full datasets.

### 3️⃣ `3_LLM_Response_Main.ipynb`
- Sends each cleaned review to a local LLM (via Ollama LLaMA3)
- Extracts:
  - Sentiment
  - Aspects
  - Pain Points
- Saves output to: `llm_output_new1.csv`

### 4️⃣ `4_LLM_Output_Standardize.ipynb`
- Standardizes extracted aspects and pain points
- Cleans LLM-generated JSON into consistent labels
- Adds columns for:
  - Standardized Category
  - Standardized Aspect
  - Standardized Pain Point
- Saves output to: `Final_dataset.csv`

### 5️⃣ `5_Final_Notebook.ipynb`
- Final cleanup and merging
- Prepares datasets for visualization/analysis
- Saves output to:
  - `Analyze_dataset1.csv`
  - `my_dataset.csv`
 
 ### 6️⃣ `Analysis.ipynb`
- Performs exploratory data analysis and insight generation
- Visualizes patterns across:
  - Price ranges
  - Manufacturers
  - Ratings and review volumes
- Generates:
  - Sunburst and treemap charts
  - Heatmaps and bar plots for aspect-level insights
  - Review-to-rating engagement metrics
  - Brand-wise and segment-wise comparisons
- Helps identify:
  - Market gaps
  - Brand positioning
  - Product opportunities

---

## 📊 Sample Dataset Columns

| Column Name                     | Description                                 |
|--------------------------------|---------------------------------------------|
| `Review Text`                  | Raw customer review                         |
| `Sentiment`                    | LLM-classified sentiment (Positive/Negative/Neutral) |
| `Aspect-PainPoint Pairs`       | LLM extracted JSON (aspect + pain)          |
| `Standardized Aspect`          | Cleaned version of aspect name              |
| `Standardized Pain Point`      | Unified wording for pain points             |
| `Verified Purchase`            | Whether the reviewer has purchased the product |
| `Rating`                       | User-provided rating (1–5 stars)            |
| `ASIN`, `Product Title`, `Price` | Product information                        |

---

## ▶️ How to Run

> 💡 This project requires:
> - Python 3.10+
> - Chrome WebDriver
> - Ollama installed and running LLaMA3 model locally

### Step 1: Start Ollama LLaMA3 locally
```bash
ollama run llama3
```

### Step 2: Run Jupyter notebooks **in order**
```
1_Extract_Amazon_Data.ipynb
2_Clean_Amazon_Data.ipynb
3_LLM_Response_Main.ipynb
4_LLM_Output_Standardize.ipynb
5_Final_Notebook.ipynb
Analysis.ipynb
```

---

## 📁 Output Files

| File Name                | Description                              |
|--------------------------|------------------------------------------|
| `product_laptop.csv`     | Raw scraped product and review data      |
| `Cleaned_laptop_df.csv`  | Cleaned reviews ready for LLM processing |
| `llm_output_new1.csv`    | LLM responses with sentiment/aspects     |
| `Final_dataset.csv`      | Standardized insights from reviews       |
| `Analyze_dataset1.csv`   | Final data for dashboard/graphs          |
| `my_dataset.csv`         | Final processed and enhanced dataset     |

---

## 📌 Features

- ✅ Scrapes product reviews from Amazon
- ✅ Cleans and preps text data
- ✅ Uses local LLM (LLaMA3 via Ollama) for insight extraction
- ✅ Standardizes messy LLM outputs
- ✅ Creates structured CSVs for business or product analysis

---

## 💬 Example Use Cases

- Identify top product issues and suggestions
- Build dashboards to visualize customer sentiments
- Understand pain points for product improvement

---

## 📥 Sample Prompt to LLM

```json
Review: "Battery drains quickly and heats up often."
LLM Output:
{
  "Sentiment": "Negative",
  "Aspects": [
    {
      "Aspect": "Battery",
      "Pain Point": "drains quickly"
    },
    {
      "Aspect": "Battery",
      "Pain Point": "Short Battery Backup"
    }
  ]
}
```

## 🧑‍💻 Author

**Pranav Kumar**  
