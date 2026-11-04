# 2026 NTU ACVSD

國立臺灣大學 2026 年 **Advanced Computer-Aided VLSI System Design（ACVSD）** 課程紀錄，包含講義、Lab、四份作業、期中與期末專題。重點涵蓋低功耗設計、跨時脈域傳輸（CDC）、匯流排、矩陣加速器、DFT 與實體設計。

## 實作導覽

| 項目 | 主題 | 主要資料 |
| --- | --- | --- |
| HW1 | Lossy Bitmask Encoder 與低功耗設計 | [規格](Homework/1/114-2_HW1.pdf)、[提交版本](Homework/1/acvsd-16-hw1-v1.tar.gz) |
| HW2 | Rotation Invariant Local Binary Pattern | [規格](Homework/2/114-2_HW2_v2.pdf)、[提交版本](Homework/2/acvsd016-hw2-v3.tar.gz) |
| HW3 | Low Power Matrix Accelerator | [說明](Homework/3/114-2_HW3_note_v3.pdf)、[提交版本](Homework/3/acvsd-16-hw3-v2.tar.gz) |
| HW4 | APR，含 scan chain 設計與 pad 整合 | [規格](Homework/4/1142_HW4_v2.pdf)、[報告](Homework/4/b11901063_report.pdf) |
| Midterm | Vision Transformer Patch Embedding Accelerator | [規格](Midterm/114-2_midterm_v1.pdf)、[提交版本](Midterm/acvsd-16-midterm-v1.tar.gz) |
| Final | Multi-Core GEMM Accelerator | [專題說明](Final/114_2_final_slide_v6.pdf)、[提交版本](Final/acvsd-hw-team5-final.tar.gz) |

## 壓縮提交版包含什麼？

- **HW1**：`top.v`、`core` 模組、RTL 檔案清單與 `top.rtl.upf`。
- **HW2**：`LBP.v`、`CORE.v`、`AXI_r.v`、`AXI_w.v` 與 `CDC.v`。
- **HW3**：`ALL` 與 `Ranking` 兩組設計，包含 SIMD／GEMM Core、共享記憶體、Interconnect、reset synchronizer 與 UPF。
- **Midterm**：`vit_pe.v`、運算核心、AXI 讀寫模組與合成／時序設定。
- **Final**：`top.sv`、`pe.sv`、`pe_config.sv`、`Router.sv`、`MAC.sv`、控制與 AXI checker 檔案，以及專題報告。

個人／團隊提交壓縮檔主要保存設計與報告。執行模擬時，須搭配同一題目的測試平台、patterns 與記憶體模型。

## 目錄結構

```text
.
├── Lecture/        # Low power、CDC、PLL、Bus、NoC、DFT、APR 與 signoff
├── Lab/
│   ├── 0/          # 工作站與 ADFP 環境
│   ├── 1/          # 低功耗設計
│   ├── 2/          # CDC 與 PLL
│   ├── 3/          # DFT 與 ATPG
│   ├── 4/          # APR (1)
│   ├── 5/          # APR (2)
│   ├── 6/          # Timing signoff
│   └── 7/          # Lab7 教材
├── Homework/1~4/    # 規格、題目環境、提交版本與報告
├── Midterm/        # ViT Patch Embedding
└── Final/          # 多核心 GEMM
```

## 環境需求

- Linux／Unix shell、`tar`／`unzip`。
- Synopsys VCS 與所需的 DesignWare 模型；部分流程需要 UPF／power-aware simulation 支援。
- Synopsys Design Compiler、Cadence Innovus，以及各 Lab 指定的驗證／signoff 工具。
- 對應的標準元件與 SRAM library；部分設定使用 N16 ADFP 與課程工作站上的 `/usr/cad/...`、`/share1/...` 路徑。

請先參考 [Lab0](Lab/0)，再核對各作業的工具環境與 library 設定。

## 快速開始：HW2 RTL 模擬

將題目環境與提交版本分開解壓，再把提交的 RTL 與檔案清單整合到測試環境：

```bash
git clone https://github.com/SR88888/2026_NTU_ACVSD.git
cd 2026_NTU_ACVSD

mkdir -p work/hw2
tar -xf Homework/2/1142_hw2_v2.tar -C work/hw2
tar -xzf Homework/2/acvsd016-hw2-v3.tar.gz -C work/hw2

cp work/hw2/b11901063_hw2/01_RTL/*.v work/hw2/1142_hw2/01_RTL/
cp work/hw2/b11901063_hw2/01_RTL/rtl_01.f work/hw2/1142_hw2/01_RTL/

cd work/hw2/1142_hw2/01_RTL
bash 01_run
```

`rtl_01.f` 會一併引用題目環境中的 AXI 模型與 `testfixture.v`。執行前請確認工作站上的 VCS 環境已載入。

## 查看期末專題

從 repository 根目錄執行：

```bash
mkdir -p work/final
tar -xzf Final/acvsd-hw-team5-final.tar.gz -C work/final
```

設計與 `report.pdf` 位於 `work/final/acvsd-hw-team5-final/`。題目配套環境另存於 [114-2-acvsd-final-v8.tgz](Final/114-2-acvsd-final-v8.tgz)；整合時請依 [專題說明](Final/114_2_final_slide_v6.pdf) 確認介面、測試流程與檔案清單。

HW3 的提交版亦引用題目環境中的 `00_TB`、SRAM 與 DesignWare。比較 `ALL`／`Ranking` 或其他版本時，請使用相同測試條件，再依當次模擬、功耗、面積與時序報告評估結果。
