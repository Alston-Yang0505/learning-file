---
layout: page
title: 📚 程式課程學習中心
---

# 歡迎來到我的線上講義


<style>
    .card-container {
        display: flex;
        gap: 20px;
        margin-top: 30px;
    }
    .card {
        flex: 1;
        padding: 20px;
        border: 1px solid #e0e0e0;
        border-radius: 12px;
        background-color: #ffffff;
        text-align: center;
        transition: transform 0.2s, box-shadow 0.2s;
        text-decoration: none !important;
        color: #333 !important;
    }
    .card:hover {
        transform: translateY(-5px);
        box-shadow: 0 10px 20px rgba(0,0,0,0.1);
        background-color: #f8fbff;
    }
    .card h2 {
        margin-top: 0;
        color: #007bff;
    }
    .card p {
        font-size: 0.9em;
        color: #666;
    }
    .btn-start {
        display: inline-block;
        margin-top: 15px;
        padding: 8px 20px;
        background-color: #007bff;
        color: white !important;
        border-radius: 5px;
        font-weight: bold;
    }
</style>

<div class="card-container">
    <a href="./matlab/ch01" class="card">
        <h2>📊 MATLAB</h2>
        <p>矩陣運算、數據繪圖與科學計算基礎。</p>
        <span class="btn-start">開始學習</span>
    </a>

    <a href="./ai/ch01" class="card">
        <h2>🤖 AI 課程</h2>
        <p>機器學習導論與神經網路實作教學。</p>
        <span class="btn-start">開始學習</span>
    </a>
</div>

---

### 📢 最新更新
- **2025-12-28**: 新增 AI 課程第二章「神經網路」。
- **2025-12-28**: 修正 MATLAB 側邊欄導覽連結。
