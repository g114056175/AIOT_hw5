# AIOT_hw5

# 🎨 AI Commercial Poster Generator (n8n Workflow) - 全自動商業海報生成器

這是一個基於 **n8n** 的自動化工作流專案。本專案修改並重構了原本僅能生成靜態圖片的基礎流程，整合了 **Google Gemini (LLM)** 的語意理解能力與 **Hugging Face FLUX.1-dev** 的強大繪圖能力，打造出一個**零成本、高品質、支援文字渲染且可批次生成**的商業海報生成系統。

> **專案起源**：本專案仿照並致敬 [AI学长小林](https://www.youtube.com/watch?v=aXocGiEx-qc) 的 n8n 自動化思路，基於其 [n8nposter.json](https://github.com/soluckysummer/n8n_workflows/blob/main/workflows/n8nposter.json) 進行深度客製化與功能增強。

---

## 📸 成果展示 (Demo)


| 工作流全覽 | 表單介面 | 生成結果範例 |
| :---: | :---: | :---: |
| ![Workflow Overview](.workflows.png) | ![Form Interface](./assets/form_ui.png) | ![Generated Poster](./assets/result_demo.png) |

---

## ✨ 核心功能 (Features)

與原版工作流相比，本專案進行了以下重大升級：

1.  **零成本方案 (Cost-Efficiency)**：
    * 移除原版昂貴的 OpenAI DALL-E 3。
    * 全面改用 **Google Gemini 1.5 Flash** (免費額度) 進行提示詞優化。
    * 改用 **Hugging Face Inference API** 調用 **FLUX.1-dev** 模型 (目前開源界最強文字渲染模型)。

2.  **文字渲染支援 (Text Rendering)**：
    * 解決了傳統 AI 繪圖無法正確寫字的問題。透過 System Prompt 工程，讓 Gemini 將中文標題轉譯為 FLUX 可識別的 `text "..."` 指令，實現在海報上精準呈現英文標題。

3.  **智能尺寸控制 (Dynamic Aspect Ratio)**：
    * 不侷限於正方形。使用者可透過選單選擇：
        * `直式海報 (9:16)`：適合 IG Reels / TikTok。
        * `正方形 (1:1)`：適合社群貼文。
        * `橫式看板 (16:9)`：適合 YouTube 封面。
        * `傳統海報 (3:4)`。
    * 後端透過 JavaScript 自動映射對應的像素 (如 768x1344)。

4.  **批次生成機制 (Batch Processing)**：
    * 支援一次生成 **1~3 張** 圖片。
    * 利用 Code 節點實作「分身機制」，為每一張圖注入獨立的 **隨機 Seed**，確保產出的多樣性。
