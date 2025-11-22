# A Job Reccommendation System Using Deep Learning BiLSTM

## 🖼️ System Workflow Diagram

```
Resume Table ──► Resume Text ──► Tokenizer ──► Resume Sequences ──►
                                                                  │
                                                                  ▼
Job Table ──► Job Text ──► Tokenizer ──► Job Sequences ───────────► Bi-LSTM Model
                                                                  │
                                                                  ▼
Positive/Negative Pairs ──► Training ──► Compatibility Score ──► Ranked Recommendations
```

- **Input:** Resume info + Job postings  
- **Processing:** Text cleaning → tokenization → padding  
- **Model:** Dual‑branch Bi‑LSTM (resume branch + job branch)  
- **Output:** Compatibility score (0–1) → Top‑N ranked jobs  

---

## ⚙️ Algorithms Used

- **Text Preprocessing**
  - Regex + BeautifulSoup for HTML cleaning
  - Tokenizer (Keras) for word → integer mapping
  - Padding sequences to fixed length

- **Feature Engineering**
  - Resume text = Major + Job History
  - Job text = Title + Description + Requirements

- **Model Architecture**
  - **Embedding Layer** (learned embeddings, 128‑dim)
  - **Bidirectional LSTM** (64 units per branch)
  - **Concatenate** resume + job vectors
  - **Dense Layer (ReLU)** for fusion
  - **Dense Output (Sigmoid)** for compatibility score

- **Training**
  - Binary Cross‑Entropy loss
  - Adam optimizer
  - Positive/Negative sampling for supervised pairs

- **Evaluation**
  - Accuracy, Precision, Recall, F1‑score
  - Confusion matrix
  - Training/validation curves

- **Recommendation**
  - Predict scores for all jobs against one resume
  - Sort by score
  - Return top‑N jobs

---

## 📋 Step‑by‑Step Procedure

1. **Data Loading**
   - Import jobs, resumes, and user history datasets.

2. **Preprocessing**
   - Clean text (remove HTML, special chars).
   - Merge resume info into `resume_text`.
   - Merge job info into `job_text`.

3. **Tokenization & Padding**
   - Fit tokenizer on both job and resume text.
   - Convert to integer sequences.
   - Pad to fixed lengths (jobs ≈ 737, resumes ≈ 32).

4. **Model Building**
   - Define two input branches (job_input, resume_input).
   - Apply embeddings + Bi‑LSTM layers.
   - Concatenate outputs.
   - Dense → Sigmoid output.

5. **Training**
   - Generate positive/negative pairs.
   - Train with batch size 32, ~10 epochs.
   - Monitor validation accuracy/loss.

6. **Evaluation**
   - Compute precision, recall, F1.
   - Visualize confusion matrix.
   - Plot accuracy/loss curves.

7. **Recommendation Generation**
   - For a given user_id, fetch resume sequence.
   - Score all jobs in test set.
   - Sort by score.
   - Return top‑N jobs with titles and descriptions.

---

## 📝 Overall Summary

This system is a **Bi‑LSTM based job recommender** that matches resumes to job postings by learning contextual embeddings of text. It processes resumes and jobs into sequences, encodes them with bidirectional LSTMs, and outputs a compatibility score. Training uses positive/negative pairs from user history. Evaluation shows strong precision/recall (~93% F1). Finally, the `recommend_jobs` function ranks jobs for a given user, and visualization presents resume info alongside top recommended jobs.

---

👉 Next, I can show you how to **package this into a one‑page project summary** (like a report for stakeholders) with diagrams + metrics + sample outputs. Would you like me to prepare that polished version?
